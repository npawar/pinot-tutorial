






# Upload table config and schema
bin/pinot-admin.sh AddTable \
  -tableConfigFile $HOME_DIR/pinot_tutorial/pinot-tutorial/transcript-table-offline.json \
  -schemaFile $HOME_DIR/pinot_tutorial/pinot-tutorial/transcript-schema.json -exec

# Upload data
bin/pinot-admin.sh LaunchDataIngestionJob \
    -jobSpecFile $HOME_DIR/pinot_tutorial/pinot-tutorial/batch-job-spec.yml
