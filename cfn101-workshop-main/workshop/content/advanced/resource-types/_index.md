---
title: 'Resource Types'
date: 2021-11-16T16:51:46Z
weight: 300
---

### Introduction

This part of the workshop focuses on how you can extend creation, provisioning, and management capabilities of [AWS CloudFormation](https://aws.amazon.com/cloudformation/) with resource types you develop.

You leverage the [AWS CloudFormation registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html) to manage extensions that you can choose to use in your account. Extensions can be public or private, and include [modules](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/modules.html), that give you the ability to encapsulate configurations and best-practice building blocks that users can describe and consume in CloudFormation templates, and [resource types](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html).

A resource type you create is treated as a first-class citizen within CloudFormation: you can manage your resource as you would manage any AWS resource.  The Software Development Life Cycle (SDLC) process of a resource type can be summarized as follows:

1. you install prerequisite tools you will use for development and testing of your resource type;
2. you start to develop and run tests for your resource type;
3. when ready, you submit the resource type to the [AWS CloudFormation registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html);
4. manage your resource type with CloudFormation: you describe the resource type and its properties in your CloudFormation template(s), like you would do with any AWS resource type.

{{% notice note %}}
You have the choice to register your resource type as a private or as a public extension in the CloudFormation registry: this lab covers private extension examples.
{{% /notice %}}

When you submit a private extension, you make it available in the AWS CloudFormation registry in your AWS account: private extensions give you the ability to test the behavior of your resource type in a sandbox environment, such as in an AWS account you own and that you use for testing/experimentation. Another use case for private extensions is for codifying private or custom application components that would be used within an enterprise, but might be company-specific, or contain proprietary logic.

You can choose to deploy your resource type in other [AWS regions using AWS CloudFormation StackSets](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/publish-extension-stacksets.html) as needed.

For more information on private extensions, see [Using private extensions in CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry-register.html). For more information on public extensions, see [Publishing extensions to make them available for public use](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/publish-extension.html).

{{% notice note %}}
Please refer to [AWS CloudFormation pricing](https://aws.amazon.com/cloudformation/pricing/) for information on charges to your account when you use private extensions or activated public extensions from third-party publishers. These charges are in addition to any charges incurred for resources that you create.
{{% /notice %}}


### Key concepts

Key concepts for developing a resource type include:

* [schema](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/resource-type-schema.html): a document where you describe your resource specification, such as properties whose input values users can specify, or read-only properties that will only be available after resource creation (for example, a resource ID), et cetera;
* [handlers](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/resource-type-develop.html#resource-type-develop-implement-handlers): when you develop a resource type, you describe its life cycle across Create, Read, Update, Delete, List (CRUDL) operations in code you will implement in a [supported language](https://github.com/aws-cloudformation/cloudformation-cli#supported-plugins). In your code, you describe the behavior you wish to have for your resource type (e.g., which AWS or third-party API to call to perform a given operation) in CRUDL handlers mentioned above (e.g., the *create* handler, the *update* handler, et cetera).
