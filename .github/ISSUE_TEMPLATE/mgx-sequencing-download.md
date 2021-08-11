---
name: MGX Sequencing Download
about: Download and archive mgx sequencing data
title: Download and archive BatchXXX
labels: Protocol Run
assignees: kescobo

---

## BatchXXX processing

Using protocol: http://klepac-ceraj-lab.github.io/drylab/download/

## Checklist

- [ ] Download the `zip` file from dropbox to the G-Drive attached to `rosalind`
  (the large Mac in the lab)
- [ ] Document the contents of the `zip` file
  - [ ] Create `batch###_details.txt`
- [ ] Extract the `zip` file into its own folder
  - [ ] Create `batch###_files.txt`
  - [ ] Create batch###.md5
- [ ] Verify that there are no conflicting file names in
  `echo/sequencing/mgx/rawfastq` or `echo/sequencing/16S/rawfastq`
- [ ] Verify that all samples included in batch have correct
  number of files (usually 8 for mgx; 4 lanes each of fwd and rev)
- [ ] Move files into `echo/sequencing/mgx/rawfastq`
- [ ] Rsync files to lovelace and ntm
