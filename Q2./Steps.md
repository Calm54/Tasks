To achieve this using GitHub Actions, we need to create a workflow that builds our project, 
generates the .pdb files, and then uploads them to an Amazon S3 bucket.

We'll need the following resources;
[x] A github repository and a .github/workflows/omit.yaml workflow file
[x] An Amazon S3 bucket from AWS
[x] A new IAM user with AmazonS3Full Access role attached to the S3 bucket (this will generate an Access Key ID & Secret Access Key)
[x] Set up AWS credentials as secrets in your GitHub repository. Go to your repository's settings and navigate to the "Secrets" section. Add the generated AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY as secrets. Provide the appropriate AWS IAM credentials with permissions to upload files to the S3 bucket.

**Defining the workflow**
```yaml
name: Publish and Upload PDB Files

   on:
     push:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Build application
           run: |
             # Add appropriate build command for your application
             # Exclude .pdb files from the build output
             # For example, using dotnet CLI:
             dotnet build --configuration Release --exclude "*.pdb"

         - name: Upload PDB files to S3
           uses: aws-actions/amazon-s3-sync@v3
           with:
             args: --exclude "*.pdb"
           env:
             AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
             AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
             AWS_REGION: S3-bucket-region
             SOURCE_DIR: ./omit/**/*.pdb
             DEST_BUCKET: S3-bucket-name
```
**Commit and push the workflow** 
Commit the omit.yml file to your repository and push it to the main branch. GitHub Actions will automatically detect the new workflow and start running it whenever there is a push event on the specified branch. Once the workflow runs successfully, the .pdb files will be uploaded to the configured S3 bucket. You can then access and download them for debugging purposes when needed.
