This repository serves as a project for deploying RustFS using Pergola. The core of this project is the `pergola.yaml` file, which acts as a Project Manifest.

A Project Manifest is a configuration file that defines the entire application stack, allowing it to be automatically built, deployed, and operated on the Pergola platform. In this specific repository, the `pergola.yaml` file details how RustFS, an S3-compatible object storage service, is containerized and configured for deployment through Pergola.

Essentially, this repository demonstrates how to use Pergola to manage and deploy an application like RustFS, leveraging Pergola's capabilities for easy, non-intrusive, instant, and secure application delivery.

For more details on Pergola Project Manifests, refer to the [official documentation](https://docs.pergola.cloud/docs/reference/project-manifest).

# About Pergola

Pergola is an application delivery platform.

It provides developers an easy and non-intrusive way of building, deploying and operating their applications. And it enables their users and customers instant and secure access to these applications.

*   **Easy**, because you don't need to setup a server or to manually install your application on a remote VM. All you need is a working application, on your machine. Then you are just a few clicks away from deploying and serving your users.
*   **Non-intrusive**, because you don't need any special changes to your application to make it work on Pergola. Your code remains agnostic and can run anywhere. All additional configuration and setup happens on Pergola and remains on Pergola.
*   **Instant**, because once deployed on Pergola, your users can access your application immediately. There is no additional access or network configuration required. Simply share the link that Pergola has supplied for your application.
*   **Secure**, because you decide who can access your application and how, whether login is required, Single-Sign-On, with enforced Multi-Factor-Authentication or without. Restrict access to specific user groups or apply fine grained role-based rules. Regardless how far you push the security constraints, all communication to and from your application is always encrypted with state of the art cryptographic protocols.

![Pergola Architecture Overview](https://docs.pergola.cloud/assets/images/pergola_architecture_overview-902224413a2ab76018064265bd7154cf.png)


# About RustFS

RustFS is a lightweight, high-performance object storage server that implements the S3 API. Built with Rust, it focuses on memory safety and speed.

## Key Features:

*   **S3 Compatibility**: Supports the S3 API for integration with existing tools and SDKs.
*   **Rust Powered**: Leverages Rust's performance and safety guarantees.
*   **Management Console**: Includes a web-based console for easy bucket and object management.
*   **Scalable Storage**: Configurable volumes and storage backends.
*   **CORS Support**: Built-in support for Cross-Origin Resource Sharing.
*   **TLS/SSL**: Native support for secure communication.
*   **Performance**: Optimized for high throughput and low latency.

For more details, visit the [RustFS project](https://github.com/rustfs/rustfs).


## Usage example


```python 
import boto3
from botocore.client import Config

s3 = boto3.client(
    's3',
    endpoint_url='https://{ingress-url}.apps.pergola.cloud/',
    aws_access_key_id='{your_access_key_id}',
    aws_secret_access_key='{your_secret_access_key}',
    config=Config(signature_version='s3v4'),
    region_name='us-east-1'
)


bucket_name = 'test'

try:
    s3.create_bucket(Bucket=bucket_name)
    print(f'Bucket {bucket_name} created.')
except s3.exceptions.BucketAlreadyOwnedByYou:
    print(f'Bucket {bucket_name} already exists.')


s3.upload_file('test.txt', bucket_name, 'text.txt')
print('File uploaded.')

```