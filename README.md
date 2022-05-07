# AI Solution Kit

## Description
The AI and ML driven applications are maturing rapidly and creating new demands on enterprises, the AI Solution Kit provides diversified leading AI/ML solutions that are easy to use. Customers can easily work with the REST API or software development kit (SDK) provided by AI/ML solution.
 
The AI Kits solution creates RESTful API for the AI features, such as SageMaker well-trained models or Lambda functions, by this solution, customers can easily pick and test a specific AI feature they like and make deployment into their account.

## Architecture

Amazon API Gateway acts as a traffic router, it creates RESTful APIs for each AI feature. The API user can invoke the RESTful APIs through the HTTPS Invoking URL endpoint, the API Gateway maps the request to the required format by the Lambda function or Amazon SageMaker endpoint, and invokes the endpoint to obtain an inference from the model, finally, it sends the prediction response(JSON format) back to the API user(client).

1. Lambda Integration

![Architecture](docs/zh/images/arch-lambda.png)

Starting from the API User(s) side, the API user sends an HTTP request to Amazon API Gateway to pass payload parameters. The API Gateway is a layer that provides the RESTful API to the client for the AI applications, ML models are stored in Amazon EFS, the AI algorithm are implemented in the Lambda function, the Lambda function parses the values from API Gateway and performs model in EFS. After that, it returns a value (JSON format) and sends it back to the API Gateway.

2. SageMaker Integration

![Architecture](docs/zh/images/arch-sagemaker.png)

The Lambda function (invoke endpoint) parses the value and sends it to the Amazon SageMaker model endpoint, the SageMaker model performs the prediction and returns the predicted value to the Lambda. The same with the Lambda implementations, the Amazon API Gateway subsequently receives the response from the Lambda function and maps it to a response that is sent back to the client.

## AI Features

| **Category**	| **Feature**  | **Description**  |
|---------------|--------------|------------------|
|Image (sync)	|[Chinese OCR](source/infer-ocr/README.md) |Support simplified/traditional Chinese, English and numbers character recognition. Recognizes text on an image as text and returns text coordinates.|
|Image (sync)	|[Inappropriate Image Detection(multi-confidence)](source/porn-image/README.md) |Dautomatically audits pictures, identifies and obtains multidimensional pornographic quantitative information (normal, sexy, porn).|
|Image (sync)	|[Image Super Resolution](source/super-resolution/README.md)	|Based on deep learning model to identify the outline of the person and body-part in the image, to separate it from the background with high accuracy segmentation.|
|Image (sync)	|[Human Image Segmentation](source/human-seg/README.md) | Segmenting human body from photo images.|

## CloudFormation Deployment

[AI Solution Kit Deployment Guide](https://aws-samples.github.io/aws-ai-solution-kit/zh/)

## Authorization and Security

By default, the AI Gateway will enable the IAM authorization and Enable the CloudWatch Logs for accessing and debugging.

## License
This project is licensed under the Apache-2.0 License.
