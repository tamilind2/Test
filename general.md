### Penetration Testing Report

#### Findings: Key Expiration Date Modification and Lack of Expiration Policy in Azure Key Vault

- **Discovery of Azure Key Vault**:
  - The attacker identified the Azure Key Vault using Azure CLI commands to enumerate resources within the subscription.
  - Command executed: `az keyvault list --output table`
  - This allowed the attacker to locate and target the Key Vault for further exploitation.

- **Modification of Key Expiration Date**:
  - The attacker, with sufficient access, was able to modify the expiration date of Customer-Managed Keys (CMKs) stored in the Azure Key Vault.
  - Command executed: `az keyvault key set-attributes --vault-name <KeyVaultName> --name <KeyName> --expires <NewExpirationDate>`
  - By altering the key expiration date, the attacker could extend the validity of a key, preventing it from expiring as intended.

- **Lack of Enforced Key Expiration and Rotation Policies**:
  - There is a lack of enforced policies to ensure regular key expiration and rotation within the Key Vault.
  - The absence of such policies means keys could remain active beyond their intended lifecycle, increasing the risk of key compromise and unauthorized access.
  - Automated key rotation may not be configured or enforced, leading to prolonged exposure of potentially compromised keys.

- **Potential Impact**:
  - **Key Misuse**: Modified expiration dates could allow the attacker to use the keys indefinitely, leading to unauthorized access to encrypted data.
  - **Extended Exposure**: Without enforced key rotation, the risk of key exposure increases over time, as compromised keys remain valid.
  - **Compliance Issues**: Failure to enforce key expiration and rotation policies may lead to non-compliance with security standards and regulations, increasing the risk of data breaches.

#### Recommendations:

- **Enforce Key Expiration Policies**: Implement and enforce policies to regularly check and validate key expiration dates, ensuring keys are invalidated and rotated as needed.
- **Automate Key Rotation (If Not Already Implemented)**: Configure automated processes to rotate CMKs periodically, reducing the risk of key compromise over time. If automation is not possible, establish a manual process with strict adherence to rotation schedules.
- **Restrict Modification Permissions**: Limit permissions for modifying key attributes, such as expiration dates, to a minimal set of trusted users to prevent unauthorized changes.
- **Monitor Key Vault Activities**: Enable detailed logging and monitoring of all activities within the Key Vault, including changes to key attributes, and set up alerts for suspicious actions.

#### Conclusion:
The vulnerabilities identified in the Azure Key Vault, including the ability to modify key expiration dates and the lack of enforced key expiration and rotation policies, significantly increase the risk of key misuse and data exposure. Implementing the recommended controls will mitigate these risks and enhance the security of key management practices within the Azure environment.
