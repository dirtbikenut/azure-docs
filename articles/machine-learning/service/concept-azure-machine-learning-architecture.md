---
title: 'Machine learning in the cloud: Terms and architecture'
titleSuffix: Azure Machine Learning service
description: Learn about the architecture, terminology, and concepts that make up Azure Machine Learning service. You also learn about the general workflow of using the service, and the Azure services that are used by Azure Machine Learning service.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.author: haining
author: hning86
ms.reviewer: larryfr
ms.date: 12/04/2018
# As a data scientist, I want to understand the big picture about how Azure Machine Learning service works.
ms.custom: seodec18
---

# How Azure Machine Learning service works: Architecture and concepts

This article describes the architecture and concepts for Azure Machine Learning service. The major components of the service and the general workflow for using the service are shown in the following diagram: 

[![Azure Machine Learning service architecture and workflow](./media/concept-azure-machine-learning-architecture/workflow.png)](./media/concept-azure-machine-learning-architecture/workflow.png#lightbox)

The workflow generally follows this sequence:

1. Develop machine learning training scripts in **Python**.
1. Create and configure a **compute target**.
1. **Submit the scripts** to the configured compute target to run in that environment. During training, the scripts can read from or write to **datastore**. And the records of execution are saved as **runs** in the **workspace** and grouped under **experiments**.
1. **Query the experiment** for logged metrics from the current and past runs. If the metrics don't indicate a desired outcome, loop back to step 1 and iterate on your scripts.
1. After a satisfactory run is found, register the persisted model in the **model registry**.
1. Develop a scoring script.
1. **Create an image** and register it in the **image registry**. 
1. **Deploy the image** as a **web service** in Azure.


> [!NOTE]
> Although this article defines terms and concepts used by Azure Machine Learning service, it does not define terms and concepts for the Azure platform. For more information about Azure platform terminology, see the [Microsoft Azure glossary](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology).

## Workspace

The workspace is the top-level resource for Azure Machine Learning service. It provides a centralized place to work with all the artifacts you create when you use Azure Machine Learning service.

The workspace keeps a list of compute targets that you can use to train your model. It also keeps a history of the training runs, including logs, metrics, output, and a snapshot of your scripts. You use this information to determine which training run produces the best model.

You register models with the workspace. You use a registered model and scoring scripts to create an image. You can then deploy the image to Azure Container Instances, Azure Kubernetes Service, or to a field-programmable gate array (FPGA) as a REST-based HTTP endpoint. You can also deploy the image to an Azure IoT Edge device as a module.

You can create multiple workspaces, and each workspace can be shared by multiple people. When you share a workspace, you can control access to it by assigning the following roles to users:

* Owner
* Contributor
* Reader

When you create a new workspace, it automatically creates several Azure resources that are used by the workspace:

* [Azure Container Registry](https://azure.microsoft.com/services/container-registry/): Registers docker containers that you use during training and when you deploy a model.
* [Azure storage account](https://azure.microsoft.com/services/storage/): Is used as the default datastore for the workspace.
* [Azure Application Insights](https://azure.microsoft.com/services/application-insights/): Stores monitoring information about your models.
* [Azure Key Vault](https://azure.microsoft.com/services/key-vault/): Stores secrets that are used by compute targets and other sensitive information that's needed by the workspace.

> [!NOTE]
> In addition to creating new versions, you can also use existing Azure services. 

A taxonomy of the workspace is illustrated in the following diagram:

[![Workspace taxonomy](./media/concept-azure-machine-learning-architecture/azure-machine-learning-taxonomy.svg)](./media/concept-azure-machine-learning-architecture/azure-machine-learning-taxonomy.png#lightbox)

## Model

At its simplest, a model is a piece of code that takes an input and produces output. Creating a machine learning model involves selecting an algorithm, providing it with data, and tuning hyperparameters. Training is an iterative process that produces a trained model, which encapsulates what the model learned during the training process.

A model is produced by a run in Azure Machine Learning. You can also use a model that's trained outside of Azure Machine Learning. You can register a model in an Azure Machine Learning service workspace.

Azure Machine Learning service is framework agnostic. When you create a model, you can use any popular machine learning framework, such as Scikit-learn, XGBoost, PyTorch, TensorFlow, Chainer, and Microsoft Cognitive Toolkit (formerly known as CNTK).

For an example of training a model, see [Quickstart: Create a Machine Learning service workspace](quickstart-get-started.md).

### Model registry

The model registry keeps track of all the models in your Azure Machine Learning service workspace. 

Models are identified by name and version. Each time you register a model with the same name as an existing one, the registry assumes that it's a new version. The version is incremented, and the new model is registered under the same name.

When you register the model, you can provide additional metadata tags and then use the tags when you search for models.

You can't delete models that are being used by an image.

For an example of registering a model, see [Train an image classification model with Azure Machine Learning](tutorial-train-models-with-aml.md).

## Image

Images provide a way to reliably deploy a model, along with all components you need to use the model. An image contains the following items:

* A model.
* A scoring script or application. You use the script to pass input to the model and return the output of the model.
* The dependencies that are needed by the model or scoring script or application. For example, you might include a Conda environment file that lists Python package dependencies.

Azure Machine Learning can create two types of images:

* **FPGA image**: Used when you deploy to a field-programmable gate array in Azure.
* **Docker image**: Used when you deploy to compute targets other than FPGA. Examples are Azure Container Instances and Azure Kubernetes Service.

For an example of creating an image, see [Deploy an image classification model in Azure Container Instances](tutorial-deploy-models-with-aml.md).

### Image registry

The image registry keeps track of images that are created from your models. You can provide additional metadata tags when you create the image. Metadata tags are stored by the image registry, and you can query them to find your image.

## Deployment

A deployment is an instantiation of your image into either a web service that can be hosted in the cloud or an IoT module for integrated device deployments. 

### Web service

A deployed web service can use Azure Container Instances, Azure Kubernetes Service, or FPGAs. You create the service from an image that encapsulates your model, script, and associated files. The image has a load-balanced, HTTP endpoint that receives scoring requests that are sent to the web service.

Azure helps you monitor your web service deployment by collecting Application Insights telemetry or model telemetry, if you've chosen to enable this feature. The telemetry data is accessible only to you, and it's stored in your Application Insights and storage account instances.

If you've enabled automatic scaling, Azure automatically scales your deployment.

For an example of deploying a model as a web service, see [Deploy an image classification model in Azure Container Instances](tutorial-deploy-models-with-aml.md).

### IoT module

A deployed IoT module is a Docker container that includes your model and associated script or application and any additional dependencies. You deploy these modules by using Azure IoT Edge on Edge devices. 

If you've enabled monitoring, Azure collects telemetry data from the model inside the Azure IoT Edge module. The telemetry data is accessible only to you, and it's stored in your storage account instance.

Azure IoT Edge ensures that your module is running, and it monitors the device that's hosting it.

## Datastore

A datastore is a storage abstraction over an Azure storage account. The datastore can use either an Azure blob container or an Azure file share as the back-end storage. Each workspace has a default datastore, and you can register additional datastores. 

Use the Python SDK API or the Azure Machine Learning CLI to store and retrieve files from the datastore. 

## Run

A run is a record that contains the following information:

* Metadata about the run (timestamp, duration, and so on)
* Metrics that are logged by your script
* Output files that are autocollected by the experiment or explicitly uploaded by you
* A snapshot of the directory that contains your scripts, prior to the run

You produce a run when you submit a script to train a model. A run can have zero or more child runs. For example, the top-level run might have two child runs, each of which might have its own child run.

For an example of viewing runs that are produced by training a model, see [Quickstart: Get started with Azure Machine Learning service](quickstart-get-started.md).

## Experiment

An experiment is a grouping of many runs from a specified script. It always belongs to a workspace. When you submit a run, you provide an experiment name. Information for the run is stored under that experiment. If you submit a run and specify an experiment name that doesn't exist, a new experiment with that newly specified name is automatically created.

For an example of using an experiment, see [Quickstart: Get started with Azure Machine Learning service](quickstart-get-started.md).

## Pipeline

You use machine learning pipelines to create and manage workflows that stitch together machine learning phases. For example, a pipeline might include data preparation, model training, model deployment, and inferencing phases. Each phase can encompass multiple steps, each of which can run unattended in various compute targets.

For more information about machine learning pipelines with this service, see [Pipelines and Azure Machine Learning](concept-ml-pipelines.md).

## Compute target

A compute target is the compute resource that you use to run your training script or host your service deployment. The supported compute targets are: 

| Compute target | Training | Deployment |
| ---- |:----:|:----:|
| Your local computer | ✓ | &nbsp; |
| Azure Machine Learning compute | ✓ | &nbsp; |
| A Linux VM in Azure</br>(such as the Data Science Virtual Machine) | ✓ | &nbsp; |
| Azure Databricks | ✓ | &nbsp; | &nbsp; |
| Azure Data Lake Analytics | ✓ | &nbsp; |
| Apache Spark for HDInsight | ✓ | &nbsp; |
| Azure Container Instances | &nbsp; | ✓ |
| Azure Kubernetes Service | &nbsp; | ✓ |
| Azure IoT Edge | &nbsp; | ✓ |
| Project Brainwave</br>(Field-programmable gate array) | &nbsp; | ✓ |

Compute targets are attached to a workspace. Compute targets other than the local machine are shared by users of the workspace.

### Managed and unmanaged compute targets

* **Managed**: Compute targets that are created and managed by Azure Machine Learning service. These compute targets are optimized for machine learning workloads. Azure Machine Learning compute is the only managed compute target as of December 4, 2018. Additional managed compute targets may be added in the future. 

    You can create machine learning compute instances directly through the workspace by using the Azure portal, the Azure Machine Learning SDK, or the Azure CLI. All other compute targets must be created outside the workspace and then attached to it.

* **Unmanaged**: Compute targets that are *not* managed by Azure Machine Learning service. You might need to create them outside Azure Machine Learning and then attach them to your workspace before use. Unmanaged compute targets can require additional steps for you to maintain or to improve performance for machine learning workloads.

For information about selecting a compute target for training, see [Select and use a compute target to train your model](how-to-set-up-training-targets.md).

For information about selecting a compute target for deployment, see the [Deploy models with Azure Machine Learning service](how-to-deploy-and-where.md).

## Run configuration

A run configuration is a set of instructions that defines how a script should be run in a specified compute target. The configuration includes a wide set of behavior definitions, such as whether to use an existing Python environment or to use a Conda environment that's built from a specification.

A run configuration can be persisted into a file inside the directory that contains your training script, or it can be constructed as an in-memory object and used to submit a run.

For example run configurations, see [Select and use a compute target to train your model](how-to-set-up-training-targets.md).

## Training script

To train a model, you specify the directory that contains the training script and associated files. You also specify an experiment name, which is used to store information that's gathered during training. During training, the entire directory is copied to the training environment (compute target), and the script that's specified by the run configuration is started. A snapshot of the directory is also stored under the experiment in the workspace.

For an example, see [Create a workspace with Python](quickstart-get-started.md).

## Logging

When you develop your solution, use the Azure Machine Learning Python SDK in your Python script to log arbitrary metrics. After the run, query the metrics to determine whether the run has produced the model you want to deploy. 

## Snapshot

When you submit a run, Azure Machine Learning compresses the directory that contains the script as a zip file and sends it to the compute target. The zip file is then extracted, and the script is run there. Azure Machine Learning also stores the zip file as a snapshot as part of the run record. Anyone with access to the workspace can browse a run record and download the snapshot.

## Activity

An activity represents a long running operation. The following operations are examples of activities:

* Creating or deleting a compute target
* Running a script on a compute target

Activities can provide notifications through the SDK or the web UI so that you can easily monitor the progress of these operations.

## Next steps

To get started with Azure Machine Learning service, see:

* [What is Azure Machine Learning service?](overview-what-is-azure-ml.md)
* [Quickstart: Create a workspace with Python](quickstart-get-started.md)
* [Tutorial: Train a model](tutorial-train-models-with-aml.md)
