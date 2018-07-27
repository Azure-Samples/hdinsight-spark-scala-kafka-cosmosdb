# How to clone this repo and contribute

This doc simply helps contributors to clone this repo and upload changes through a pull request.

## Install tools to use git locally:

- You can use Git bash command line to run these commands. 

   [Git SCM download](https://git-scm.com/downloads)

- VS Code has a nice graphical interface to interact with git and GitHub as well. 

   [Visual Studio Code download](https://code.visualstudio.com/download)

## Initial first time local clone:
1. Visit the sample repo URL and click Fork. Choose your account as the destination. This makes a cloud copy into your own fork.

   [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb/](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb/)

2. Clone the forked repo locally on your box:
```git bash
mkdir /c/git/Azure-Samples
cd /c/git/Azure-Samples
git clone https://YourUserName@github.com/YourUserName/hdinsight-spark-scala-kafka-cosmosdb.git
cd hdinsight-spark-scala-kafka-cosmosdb
```

## Subsequent use:
1. Periodically, update your local copy with a sync from the master branch of the upstream repo (not your fork).

```git bash
cd /c/git/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb
git pull https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb.git master
```

2. Edit the files locally on your box. 

3. Once you are done editing, add the files you want to keep from your staging area, and commit that change.

```git bash
git add . 
git status 
git commit -m"Changing something"
```

4. Push the local commit up to the cloud fork.

```git bash
git push origin master
```

5. Using a browser, issue a pull request to merge from your fork into the upstream. (master branch by default)

   [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb/compare?expand=1](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb/compare?expand=1)
