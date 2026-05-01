# ISO 27001 Controls

!!! danger "Disclaimer"

    The information provided in this document is for general informational purposes only. Any liability for the completeness, accuracy, timeliness, or reliability of the content is expressly excluded. Organizations are advised to consult with legal, compliance, or technical experts to ensure that their specific compliance and security needs are adequately addressed.

ISO 27001, an international standard for information security, includes 14 domains and 114 controls aimed at protecting information assets. {{ product_name }} plays a critical role in enabling compliance with these controls by focusing on the technical aspects of Kubernetes-based workloads.

- Total Domains in ISO 27001: 14
- Total Controls in ISO 27001: 114

## Controls Addressed by {{ product_name }}

- **Directly Applicable Controls**: {{ product_name }} enables the implementation of 28 controls, fully enforceable through Kubernetes configurations and features. These controls span critical areas such as:

    - **Access Control (A.9)**: Implementing Role-Based Access Control (RBAC) and restricting unauthorized access to resources.
    - **Cryptography (A.10)**: Ensuring data security through encryption and robust key management.
    - **Operations Security (A.12)**: Automating vulnerability scanning, logging, and secure cluster configurations.
    - **Communications Security (A.13)**: Securing inter-service communication with encrypted traffic and network isolation.

- **Partially Applicable Controls**: An additional 22 controls are partially supported by {{ product_name }} through integrations and configurable policies. For example:

    - **Information Security Policies (A.5)**: {{ product_name }} helps align Kubernetes policies with organizational security frameworks.
    - **Supplier Relationships (A.15)**: Ensures the use of trusted container images and compliance checks for third-party integrations.

{{ product_name }} directly or partially addresses approximately **50 controls** across ISO 27001’s domains, enabling organizations to align their Kubernetes-based workloads with best practices for security, availability, and compliance. By focusing on technical measures and leveraging Kubernetes features, {{ product_name }} simplifies the complex task of meeting international security standards.

This support makes {{ product_name }} a useful tool for organizations aiming to achieve ISO 27001 compliance in modern cloud-native environments.
