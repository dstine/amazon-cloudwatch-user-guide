# Verify the Signature of the CloudWatch Agent Package<a name="verify-CloudWatch-Agent-Package-Signature"></a>

GPG signature files are included for CloudWatch Agent packages\. You can use the public key to verify that the agent download file is original and unmodified\. First, import the public key with [https://gnupg.org/index.html](https://gnupg.org/index.html)\.

To find the correct signature file, see the following table: 


| Arch | Platform | Download Link | Signature File Link | 
| --- | --- | --- | --- | 
|  amd64 |  Amazon Linux and Amazon Linux 2  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/amazon\_linux/amd64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/amazon\_linux/amd64/latest/amazon\-cloudwatch\-agent\.rpm\.sig  | 
|  amd64 |  Centos  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/centos/amd64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/centos/amd64/latest/amazon\-cloudwatch\-agent\.rpm\.sig  | 
|  amd64 |  Redhat  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/redhat/amd64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/redhat/amd64/latest/amazon\-cloudwatch\-agent\.rpm\.sig  | 
|  amd64 |  SUSE  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/suse/amd64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/suse/amd64/latest/amazon\-cloudwatch\-agent\.rpm\.sig  | 
|  amd64 |  Debian  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/debian/amd64/latest/amazon\-cloudwatch\-agent\.deb  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/debian/amd64/latest/amazon\-cloudwatch\-agent\.deb\.sig  | 
|  amd64 |  Ubuntu  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/ubuntu/amd64/latest/amazon\-cloudwatch\-agent\.deb  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/ubuntu/amd64/latest/amazon\-cloudwatch\-agent\.deb\.sig  | 
|  amd64 |  Windows  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/windows/amd64/latest/amazon\-cloudwatch\-agent\.msi  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/windows/amd64/latest/amazon\-cloudwatch\-agent\.msi\.sig  | 
|  arm64 |  Amazon Linux 2  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/amazon\_linux/arm64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/amazon\_linux/arm64/latest/amazon\-cloudwatch\-agent\.rpm\.sig  | 
|  arm64 |  Redhat  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/redhat/arm64/latest/amazon\-cloudwatch\-agent\.rpm  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/redhat/arm64/latest/amazon\-cloudwatch\-agent\.rpm\.sig   | 
|  arm64 |  Ubuntu  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/ubuntu/arm64/latest/amazon\-cloudwatch\-agent\.deb  |  https://s3\.amazonaws\.com/amazoncloudwatch\-agent/ubuntu/arm64/latest/amazon\-cloudwatch\-agent\.deb\.sig   | 

**To verify the CloudWatch agent package on a Linux server**

1. Download the public key\.

   ```
   shell$ wget https://s3.amazonaws.com/amazoncloudwatch-agent/assets/amazon-cloudwatch-agent.gpg
   ```

1. Import the public key into your keyring\.

   ```
   shell$  gpg --import amazon-cloudwatch-agent.gpg
   gpg: key 3B789C72: public key "Amazon CloudWatch Agent" imported
   gpg: Total number processed: 1
   gpg: imported: 1 (RSA: 1)
   ```

   Make a note of the key value, as you need it in the next step\. In the preceding example, the key value is `3B789C72`\.

1. Verify the fingerprint by running the following command, replacing *key\-value* with the value from the preceding step:

   ```
   shell$  gpg --fingerprint key-value
   pub   2048R/3B789C72 2017-11-14
         Key fingerprint = 9376 16F3 450B 7D80 6CBD  9725 D581 6730 3B78 9C72
   uid                  Amazon CloudWatch Agent
   ```

   The fingerprint string should be equal to the following:

   `9376 16F3 450B 7D80 6CBD 9725 D581 6730 3B78 9C72`

   If the fingerprint string does not match, do not install the agent, and contact Amazon Web Services\.

   After you have verified the fingerprint, you can use it to verify the signature of the CloudWatch agent package\.

1. Download the package signature file using wget\. To determine the correct signature file, see the preceding table\.

   ```
   wget Signature File Link
   ```

1. To verify the signature, run `gpg --verify`\.

   ```
   shell$ gpg --verify signature-filename agent-download-filename
   gpg: Signature made Wed 29 Nov 2017 03:00:59 PM PST using RSA key ID 3B789C72
   gpg: Good signature from "Amazon CloudWatch Agent"
   gpg: WARNING: This key is not certified with a trusted signature!
   gpg:          There is no indication that the signature belongs to the owner.
   Primary key fingerprint: 9376 16F3 450B 7D80 6CBD  9725 D581 6730 3B78 9C72
   ```

   If the output includes the phrase `BAD signature`, check whether you performed the procedure correctly\. If you continue to get this response, contact Amazon Web Services and avoid using the downloaded file\.

   Note the warning about trust\. A key is only trusted if you or someone that you trust has signed it\. This does not mean that the signature is invalid, only that you have not verified the public key\.

**To verify the CloudWatch agent package on a server running Windows Server**

1. Download and install GnuPG for Windows from [https://gnupg.org/download/](https://gnupg.org/download/)\. When installing, include the **Shell Extension \(GpgEx\)** option\.

   The remaining steps can be performed in Windows PowerShell\.

1. Download the public key\.

   ```
   PS> wget https://s3.amazonaws.com/amazoncloudwatch-agent/assets/amazon-cloudwatch-agent.gpg -OutFile amazon-cloudwatch-agent.gpg
   ```

1. Import the public key into your keyring\.

   ```
   PS>  gpg --import amazon-cloudwatch-agent.gpg
   gpg: key 3B789C72: public key "Amazon CloudWatch Agent" imported
   gpg: Total number processed: 1
   gpg: imported: 1 (RSA: 1)
   ```

   Make a note of the key value, as you need it in the next step\. In the preceding example, the key value is `3B789C72`\.

1. Verify the fingerprint by running the following command, replacing *key\-value* with the value from the preceding step:

   ```
   PS>  gpg --fingerprint key-value
   pub   rsa2048 2017-11-14 [SC]
         9376 16F3 450B 7D80 6CBD  9725 D581 6730 3B78 9C72
   uid           [ unknown] Amazon CloudWatch Agent
   ```

   The fingerprint string should be equal to the following:

   `9376 16F3 450B 7D80 6CBD 9725 D581 6730 3B78 9C72`

   If the fingerprint string does not match, do not install the agent, and contact Amazon Web Services\.

   After you have verified the fingerprint, you can use it to verify the signature of the CloudWatch agent package\.

1. Download the package signature file using wget\. To determine the correct signature file, see [CloudWatch Agent Download Links](install-CloudWatch-Agent-on-onprem.md#agent-download-link-table)\.

1. To verify the signature, run `gpg --verify`\.

   ```
   PS> gpg --verify sig-filename agent-download-filename
   gpg: Signature made 11/29/17 23:00:45 Coordinated Universal Time
   gpg:                using RSA key D58167303B789C72
   gpg: Good signature from "Amazon CloudWatch Agent" [unknown]
   gpg: WARNING: This key is not certified with a trusted signature!
   gpg:          There is no indication that the signature belongs to the owner.
   Primary key fingerprint: 9376 16F3 450B 7D80 6CBD  9725 D581 6730 3B78 9C72
   ```

   If the output includes the phrase `BAD signature`, check whether you performed the procedure correctly\. If you continue to get this response, contact Amazon Web Services and avoid using the downloaded file\.

   Note the warning about trust\. A key is only trusted if you or someone that you trust has signed it\. This does not mean that the signature is invalid, only that you have not verified the public key\.