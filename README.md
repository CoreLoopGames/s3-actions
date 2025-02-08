# Download from S3 using AWS CLI

This composite action downloads files from an S3 bucket using the AWS CLI.

## Inputs

- `aws-access-key-id` (required): AWS Access Key ID.
- `aws-secret-access-key` (required): AWS Secret Access Key.
- `aws-region` (required, default: `us-east-1`): AWS Region.
- `s3-bucket` (required): S3 Bucket Name.
- `s3-key` (required): S3 key (path) of the file to download.
- `local-path` (required): Local path where to save the downloaded file.

## Usage

```yaml
jobs:
  download_job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Download from S3
        uses: your-username/your-repo/download@main
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
          s3-bucket: your-bucket-name
          s3-key: path/to/your/file
          local-path: path/to/save/file


**Lookup Action (`lookup/README.md`):**

```markdown
# Check S3 File Existence

This composite action checks if a file exists in an S3 bucket using the AWS CLI.

## Inputs

- `aws-access-key-id` (required): AWS Access Key ID.
- `aws-secret-access-key` (required): AWS Secret Access Key.
- `aws-region` (required, default: `us-east-1`): AWS Region.
- `s3-bucket` (required): S3 Bucket Name.
- `s3-key` (required): S3 key (path) to check.

## Outputs

- `file-exists`: Indicates whether the file exists in S3 (`true` or `false`).
- `file-metadata`: Metadata of the file if it exists; `null` if it does not.

## Usage

```yaml
jobs:
  lookup_job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Check S3 File Existence
        id: check_file
        uses: your-username/your-repo/lookup@main
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
          s3-bucket: your-bucket-name
          s3-key: path/to/your/file

      - name: Use Output
        run: |
          if [ "${{ steps.check_file.outputs.file-exists }}" == "true" ]; then
            echo "File exists. Metadata: ${{ steps.check_file.outputs.file-metadata }}"
          else
            echo "File does not exist."
          fi
