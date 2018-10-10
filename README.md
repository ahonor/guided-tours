
# Usage

The `build-tour` command reads a directory of tour content files and writes JSON loadable to the guided tour feature.
The JSON data is written to stdout and can be redirected to the file you will copy to the Rundeck install.

The command's basic usage is shown below:

```
build-tour --source-dir <> [--name <> [--key <>]]
```

Example: 

`build-tour --source-dir ./navigation > navigation-tour.json`


# Tour content

The tour's content structure contains one or more markdown files. 
Each markdown file represents a step in the tour. 

## Step content


The build-tour command also can interpret the
topic from the filename using the syntax _{NN}_-_{topic}_.md (eg, 00-stepA.md).

The numeric prefix is a file naming convention to define the order of the tour steps.

```
<tour basedir>
├── 00-stepA.md
├── 01-stepB.md
└── 0N-stepN.md
```

To have better control over topic naming (eg, a space separated topic name) use following comment style at the top of the file to specify the step's title. 

```
<!--
#/ title: MyTopic
-->
```