---
layout: post
title: "What's New in ML.NET"
tags: ["ml.net","machinelearning","ai"]
---

[← Previous: What’s new in ASP.NET Core 9.0](/5-whats-new-in-aspnet-core-9-0)  
ML.NET continues to evolve as a full-featured, open-source machine learning framework for .NET developers, enabling you to create, train, and deploy custom ML models directly in your .NET applications. ML.NET 3.0 and 4.0 bring expanded capabilities for advanced AI scenarios—particularly around deep learning tasks, AutoML improvements, and enhanced tokenization support—making it easier to handle complex text and vision problems.

## New Deep-Learning Tasks

**Deep Learning with TorchSharp**  
ML.NET 3.0 introduces support for several new deep-learning tasks backed by TorchSharp, a .NET library for PyTorch-based deep learning. These tasks include:

- **Object Detection:** Automatically identify objects within images, assigning bounding boxes and categories. This enables a range of computer vision scenarios, from product detection in e-commerce images to recognizing signs in autonomous driving footage.
- **Named Entity Recognition (NER):** Extract entities like names, places, organizations, and more from text. NER models streamline text processing, making it easier to process documents, support chatbots, and enhance search functionality.
- **Question Answering (QA):** Build systems capable of reading comprehension—answering questions about given documents or passages. This feature has significant implications for building chatbots, documentation Q&A tools, and intelligent search solutions.

All these trainers are included in the `Microsoft.ML.TorchSharp` package. For more details, check out the [Announcing ML.NET 3.0](https://devblogs.microsoft.com/dotnet/announcing-ml-net-3-0/) post.

## AutoML Enhancements

AutoML (Automated Machine Learning) simplifies model selection and hyperparameter tuning by automating the training and evaluation pipeline. ML.NET 3.0 updates the AutoML sweeper to handle new tasks, including sentence similarity, question answering, and object detection. With these improvements, you can quickly experiment with various models and configurations using the AutoML API, reducing the time and expertise required to achieve state-of-the-art results.

For more information, see [How to use the ML.NET Automated Machine Learning (AutoML) API](https://learn.microsoft.com/dotnet/machine-learning/how-to-guides/howto-use-automl-api).

## Enhanced Tokenizer Support

Text tokenization is a crucial step in NLP pipelines, splitting raw text into manageable tokens (words, subwords, or symbols) before feeding it into language models. In ML.NET 4.0, the `Microsoft.ML.Tokenizers` package introduces significant enhancements:

- **Refined APIs and Tiktoken Support:**  
  The tokenizer library now supports Tiktoken (the tokenization method used by OpenAI models), enabling more accurate and efficient tokenization for GPT models, such as GPT-4. This lets you integrate local or remote AI services easily, better understand your costs (e.g., Azure OpenAI tokens), and manage prompt context sizes.

- **Llama Model Tokenizer:**  
  The library now supports tokenizing text for Llama-based models, enabling usage of models like LLaMA and Mistral with minimal extra tooling.

- **CodeGen Tokenizer:**  
  With support for CodeGen tokenizers (compatible with models such as codegen-350M-mono and phi-2), you can tokenize code-oriented data and build advanced coding assistants or code-search solutions.

- **Span-based APIs and Flexible Normalization:**  
  New overloads accept `Span<char>` inputs and allow you to toggle normalization and pretokenization steps. These capabilities give fine-grained control over how text is processed, improving performance and adaptability for various NLP workflows.

- **Migration from DeepDev or SharpToken:**  
  The ML.NET tokenization ecosystem has consolidated around Microsoft.ML.Tokenizers. If you’ve previously used DeepDev or SharpToken, a migration guide is provided to help you smoothly transition to `Microsoft.ML.Tokenizers`.

For examples and more details, see [Announcing ML.NET 2.0](https://devblogs.microsoft.com/dotnet/announcing-ml-net-2-0/) and the updated [tokenization library documentation](https://learn.microsoft.com/dotnet/machine-learning/how-to-guides/).

## Model Builder in Visual Studio

Model Builder, the Visual Studio extension that provides a UI-based machine learning workflow, now consumes ML.NET 3.0. Starting from Model Builder version 17.18.0, you can leverage newly introduced scenarios like question answering (QA) and named entity recognition (NER) directly within Visual Studio. This streamlines building advanced NLP pipelines without leaving your IDE.

---

In summary, ML.NET’s recent updates extend the framework’s capabilities into advanced AI tasks such as object detection, NER, and QA, while improving automation via AutoML and simplifying text preprocessing with enhanced tokenization. These updates open the door to more sophisticated and production-ready machine learning solutions directly integrated into your .NET applications.
[Next → What’s New in .NET MAUI for .NET 9](/7-whats-new-in-dotnet-maui-for-dotnet-9)
**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)