# Set BASE_DIR
BASE_DIR=`pwd`

# Upload table config and schema
bin/pinot-admin.sh AddTable \
  -tableConfigFile $BASE_DIR/transcript-table-offline.json \
  -schemaFile $BASE_DIR/transcript-schema.json -exec

# Upload data
bin/pinot-admin.sh LaunchDataIngestionJob \
    -jobSpecFile $BASE_DIR/batch-job-spec.yml
