## Create a new bucket

``
aws s3 mb s3://checksums-solutionsarchitect-mb-1234
```

## Create file to checksum

```
echo "Hello Mars" > myfile.txt
```

## Get a checksum of a file

```
md5sum myfile.txt

which returns 8ed2d86f12620cdba4c976ff6651637f *myfile.txt
```

## Upload file and look at its etag

```
aws s3 cp myfile.txt s3://checksums-solutionsarchitect-mb-1234
aws s3api head-object --bucket s3://checksums-solutionsarchitect-mb-1234 --key myfile.txt

which returns the md5 ETag of the object, which "could" be used for the checksum, but could be better to use AWS's other options
```

## Let's upload a file with a different kind of checksum (CRC32 in this case) *not working, unforch
```
sha1sum myfile.txt
aws s3api put-object --bucket checksums-solutionsarchitect-mb-1234 \
--key myfilesha.txt \
--body myfile.txt \
--checksum-sha1 c28ccc2c5e214036806014df9fb43634f3e770b2
```