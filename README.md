```console
$ git init
$ dvc init
$  dvc add < path to data>
$ cat data/.gitignore # to show thata the data is not being tracked
$ git add data/datafile.dvc data/.gitignore # we send the datafile.dvc to git instead of the data. This is how both data stay connected
```

- Examine data/.gitignore to show that the data is not being sent to git
- set up remote storage for data versioning

```console
$ git status # to show files in the staging area
$ git commit both data/datafile.dvc data/.gitignore
$ cat data/datafile.dvc # to see the cryptic name created to rep the file
$ dvc remote add -d  dvcOrigin < to storage location>
$ cat .dvc/config   # shows the remote location in our config file
$ git commit -m " Configure the remote storage for dvc" # commit the configuration file
$ dvc push    # push file to remote storage
```

## Our first Data Versioning Demo

### Let us delete our raw data and dvc/cache

```console
$ rm -f raw_data/fake_file.csv # remove the raw dataset file
$ rm -rf .dvc/cache/   # remove the dvc cache
$ ls raw_data   # show that the data is deleted
$ dvc pull     # to bring back the raw dataset
```

## Our first Data Versioning Demo

### Let us change the data. In this case we will double the size of the dataset

```console
$ cp raw_data/fake_file.csv /tmp/fake_file.csv      # copy the dataset to another directory
$ cp raw_data/fake_file.csv ./tmp/fake_file.csv  # confirm copied data
$ ls -lh raw_data/fake_file.csv
$ ls -lh tmp/fake_file.csv # Check the saize of the dataset
$ cat tmp/fake_file.csv >> raw_data/fake_file.csv  # concatenate the dataset
$ $ ls -lh raw_data/fake_file.csv # check the size again to make sure this is done
$ dvc add raw_data/fake_file.csv # add the new file
$ git add raw_data/fake_file.csv.dvc   # track with git
$ git status
$ git commit -m "A new file was receievd from data owner"
$ dvc push # pushes the new file to our remote storage
$ git checkout HEAD~1 raw_data/fake_file.csv.dvc  # checkout theoriginal file
$ dvc checkout # we do not need to do "dvc add" after this one cos we already have a copy of this version in storage
```

**Now we have two versions of the same data set in our remote storage**. We can go back and forth between these datasets

```console
$ git checkout HEAD~1 raw_data/fake_file.csv.dvc  # check out the .dvc here
$ dvc checkout
$ ls -lh raw_data/fake_file.csv # check the size again
$ git commit -m "Revert back to the raw dataset"  # commit the new .dvc file
```

## Let us add a git remote

~~$ git checkout -b hadev # check out your development branch~~

```console
$ git remote add origin <remote url> # add remote
$ git branch -M main # sets the main path from the main branch
$ git push -u origin main #
```

- Examine the remote branch

# Sharing datasets and files
