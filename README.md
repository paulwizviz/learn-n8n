# Our Journey with n8n: Working Examples and Discoveries

Welcome to our project! This is where we're documenting our journey as we explore n8n, the open-source workflow automation platform. We think of n8n as a digital assembly line, a place where we can connect different applications and services to automate away the repetitive tasks and build some rather complex data pipelines. Everything is built on a visual, node-based editor, where each "node" is a step—an action, a trigger, or a data transformation—in our workflow.

As we've been working with it, a few key things have really stood out to us:

* **Low-Code, but with Power:** We've found the balance here to be just right. We can quickly piece together workflows with the drag-and-drop interface and pre-built nodes, which is fantastic. But when we need to get our hands dirty, n8n lets us drop in custom JavaScript or Python code. It’s a hybrid approach that seems to work well for everyone, regardless of their technical background.

* **The Freedom of Self-Hosting:** This was a massive plus for us. Being able to deploy n8n on our own infrastructure (we're using Docker, but Kubernetes is also an option) gives us complete control over our data. It's a level of security and freedom from vendor lock-in that we really appreciate. Of course, there's a managed cloud version if you prefer to let someone else handle the hosting.

* **Built for AI:** We're excited about the possibilities with AI, and n8n is clearly built with this in mind. It has built-in AI nodes that connect to large language models (LLMs) like OpenAI, Gemini, and Claude. We're looking forward to creating some sophisticated AI agents for things like content generation and data analysis.

* **Connecting Everything:** The library of over 400 pre-built integrations is impressive, and the community is always adding more. We've been able to connect to almost every app and database we've needed. For anything else, the trusty HTTP Request node lets us connect to any API we come across.

## Notes

* [Deployments](./deployments/doc.md)

## Disclaimer

This project is for educational purposes only. It is not a production-ready solution and requires significant modifications, rigorous security audits, and extensive testing for use in a production environment.

This project is ongoing and subject to changes without prior notice. By using this project, you acknowledge that you do so at your own risk. The authors of this project accept no liability for any issues or damages resulting from its use. Please use this project as a learning resource, and not as a fully functional or secure application.

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

Copyright 2024 The Contributors to `learn-n8n`

Please refer to the CONTRIBUTORS file for a list of contributors or the repository's commit history.
