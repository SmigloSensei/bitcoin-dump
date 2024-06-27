# Information
Dumps the entire blockchain or a sequence of blocks in human readable format JSON.<br />
The output directory is controlled by DUMP_BLOCK_DIR.

# Usage
`bitcoin-dump`                 - Dumps the entire blockchain.<br />
`bitcoin-dump [START] [END]`   - Drops a sequence of blocks.

> [!WARNING]
> - JSON files that already exist are skipped.
> - JSON files from the most recent blocks in the blockchain are unreliable, which is why SAFE_BLOCK_MARGIN exists.

To count files with 0 size use (e.g. out of disk space during the dump):<br>
`find blocks -type f -size 0 | wc -l`

To delete files with 0 size use (and recreate by 2nd bitcoin-dump):<br>
`find blocks -type f -size 0 -delete`

To count txids in a block use:<br>
`cat $DUMP_BLOCK_FILE | grep nTx | grep -Po "\d*"`

To extract txids from a block use:<br>
`tail -n $[$(cat $DUMP_BLOCK_FILE | grep nTx | grep -Po "\d*")+2] $DUMP_BLOCK_FILE | grep -Po "[a-z0-9]*"`
