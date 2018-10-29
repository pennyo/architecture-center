---
title: Image classification with Convolutional Neural Networks 
description: Explore transfer learning, convolutional neural networks, and gradient-boosting decision tree algorithms.
author: adamboeglin
ms.date: 10/29/2018
---
# Image classification with Convolutional Neural Networks 
Lean manufacturing, cost control, and waste reduction are imperative for manufacturing to remain competitive. In circuit-board manufacturing, faulty boards can cost manufacturers money and productivity. Assembly lines rely on human operators to quickly review and validate boards flagged as potentially faulty by assembly-line test machines.
This solution analyzes electronic component images generated by assembly-line cameras in a circuit-board manufacturing plant and detects their error status. The goal is to minimize or remove the need for human intervention. The solution builds an image classification system using a convolutional neural network with 50 hidden layers, pretrained on 350,000 images in an ImageNet dataset to generate visual features of the images by removing the last network layer. These features are then used to train a boosted decision tree to classify the image as pass or fail and final scoring conducted on edge machines at the plant. The classification performance results are good (time-based cross-validation AUC>.90) which indicates the solution is suitable to drastically minimize human intervention for electronic-components failure detection in assembled circuit boards.
Using this solution to automate failure detection instead of relying solely on human operators helps improve the identification of faulty electronic components and boost productivity.

## Architecture
<img src="media/image-classification-with-convolutional-neural-networks.svg" alt='architecture diagram' />

## Components
* Azure Blob Storage: Data is ingested and stored in Azure Blob Storage.
* GPU based Azure Data Science Virtual Machine: The core development environment is the Azure Ubuntu-based GPU DSVM. The data is pulled from blob onto an Azure virtual hard disk (VHD) attached to the DSVM. On that VHD, the data is processed, the images are featurized using a Deep Neural Network, and a Boosted Tree model is trained. DSVM IPython Notebook server is used for solution development.
* Azure Batch AI training (BAIT): As an alternative to DSVM-based training, for computing-intensive jobs that use deep-learning image processing, we use BAIT as a managed Azure Batch framework for
parallel and distributed computing using clusters of GPU compute nodes.
* Microsoft Machine Learning for Apache Spark HDInsight Spark Cluster: As an alternative to DSVM-based training, for big datasets, we use MMLSpark to build a highly scalable training solution.
* Azure Container Registry: The model and web application are packaged into a Docker image and written to Azure Container Registry.
* Azure Machine Learning Model Management Service
* Azure Container Service Cluster: Deployment for this solution uses Azure Container Service running a Kubernetes-managed cluster. The containers are deployed from images stored in Azure Container Registry.

## Next Steps
* [Learn more about Azure Blob Storage](href="http://azure.microsoft.com/services/storage/blobs/)
* [Learn more about Data Science Virtual Machine](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.windows-data-science-vm?tab=Overview)
* [Learn more about Batch AI Training](href="http://azure.microsoft.com/roadmap/azure-batch-ai-training-for-deep-learning-models/)
* [Browse on Github](https://github.com/azure/mmlspark)
* [Learn more about Azure Container Registry](href="http://azure.microsoft.com/services/container-registry/)
* [Learn more about Model Management](https://docs.microsoft.com/azure/machine-learning/preview/model-management-overview)
* [Learn more about Azure Container Service](href="http://azure.microsoft.com/services/container-service/)