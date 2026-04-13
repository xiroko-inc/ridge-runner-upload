# Document Upload Instructions

## What You Need

1. The `ridge-runner-upload.exe` file (provided to you)
2. Your AWS credentials (Access Key ID and Secret Access Key — provided separately)
3. Your documents folder

That's it. No install, no setup, no AWS CLI.

## Uploading Documents

**Option A — Environment variables (recommended):**

1. Open **Command Prompt** or **PowerShell**
2. Set your credentials:

   **Command Prompt:**
   ```
   set AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY
   set AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
   ```

   **PowerShell:**
   ```
   $env:AWS_ACCESS_KEY_ID="YOUR_ACCESS_KEY"
   $env:AWS_SECRET_ACCESS_KEY="YOUR_SECRET_KEY"
   ```
3. Run the upload tool:
   ```
   ridge-runner-upload.exe "C:\Path\To\Your\Documents"
   ```

**Option B — Flags:**

```
ridge-runner-upload.exe --access-key YOUR_ACCESS_KEY --secret-key YOUR_SECRET_KEY "C:\Path\To\Your\Documents"
```

Replace `YOUR_ACCESS_KEY` and `YOUR_SECRET_KEY` with the credentials you were given.

The tool will:
- Scan for all supported file types
- Show a summary of what it found
- Ask you to confirm before uploading
- Upload to the secure S3 bucket
- Skip files that haven't changed (safe to re-run anytime)
- Preserve your folder structure

## Preview First (Optional)

To see what would be uploaded without actually uploading:

```
ridge-runner-upload.exe --dry-run "C:\Path\To\Your\Documents"
```

No credentials needed for a dry run.

## Supported File Types

| Type | Extensions |
|------|-----------|
| Word | .docx, .doc |
| Excel | .xlsx, .xls |
| PowerPoint | .pptx, .ppt |
| PDF | .pdf |
| Text | .txt, .csv, .tsv |
| ArcGIS | .shp, .dbf, .shx, .prj, .cpg, .sbn, .sbx, .geojson, .gpkg, .gdb (directories) |

## Troubleshooting

- **"credentials required"** — provide credentials via `--access-key`/`--secret-key` flags or set `AWS_ACCESS_KEY_ID`/`AWS_SECRET_ACCESS_KEY` environment variables
- **"source directory does not exist"** — check the path, use quotes if it contains spaces
- **"access denied" or "forbidden"** — check with the project admin that your credentials are active
- **Upload seems stuck** — large files take time. The tool shows each file as it uploads. Press Ctrl+C to cancel safely.

## Re-Running

You can re-run the tool anytime. It skips files that already exist in S3 with the same size, so only new or changed files are uploaded.
