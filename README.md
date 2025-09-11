# **Testing ScoutSuite for AWS Security Assessment**


## **Step 1: Setting up AWS CLI**
To allow ScoutSuite to access the AWS instance, the AWS Command Line Interface (CLI) was configured:

1. Installed AWS CLI on Windows using the official installer.
2. Configured AWS credentials using the provided IAM user account:

```powershell
aws configure
```
Entered the following:
- **AWS Access Key ID**: Provided by lab instructions
- **AWS Secret Access Key**: Provided by lab instructions
- **Region**: eu-north-1
- **Output format**: json
```
aws sts get-caller-identity
```
Verified that the CLI could authenticate successfully. Example output:
```json
{
    "UserId": "AIDASJGAAPVA6JJ3EHC5L",
    "Account": "157168991553",
    "Arn": "arn:aws:iam::157168991553:user/mason"
}
```
This confirms that the IAM user `mason` has valid credentials and can be used with ScoutSuite.

---

## **Step 2: Downloading and Configuring ScoutSuite**
1. Cloned ScoutSuite repository from GitHub:
```powershell
git clone https://github.com/nccgroup/ScoutSuite.git
cd ScoutSuite
```
2. Installed Python dependencies:
```powershell
pip install -r requirements.txt
```
3. Verified that Python 3.6+ and pip were installed and working.

---

## **Step 3: Running ScoutSuite**
1. Ran ScoutSuite using the configured AWS profile:
```powershell
python scout.py aws --profile default --regions eu-north-1
```
2. ScoutSuite generated an HTML report in the `scoutsuite-report` folder.
3. Opened the HTML report in a browser to review security misconfigurations, IAM policies, and cloud resource information.

### **Notes on Permissions**
- The provided IAM user had restricted permissions, causing some warnings in ScoutSuite for services such as EC2 and CloudFormation.
- To avoid unnecessary errors, the scan can be limited to accessible services with:
```powershell
python scout.py aws --profile default --regions eu-north-1 --services s3 --services iam --services ses --services sns --services sqs --services vpc
```

---

## **Conclusion**
By configuring AWS CLI with the provided IAM credentials and running ScoutSuite, a read-only security audit of the AWS instance was successfully performed. This method ensures cloud security without altering resources and provides a clear report for identifying potential misconfigurations.

---

## **References (Harvard Anglia style)**
- NCC Group, 2024. ScoutSuite: Multi-cloud security auditing tool. [GitHub] Available at: <https://github.com/nccgroup/ScoutSuite> [Accessed 8 September 2025].
- Amazon Web Services, 2025. AWS Command Line Interface. [online] Available at: <https://aws.amazon.com/cli/> [Accessed 8 September 2025].
- YouTube, 2024. AWS CLI Setup Tutorial. [video online] Available at: <https://youtu.be/jCHOsMPbcV0> [Accessed 8 September 2025].

