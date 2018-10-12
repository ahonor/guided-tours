
# Guided Tours
## Usage

The `build-tour` command reads a directory of markdown files and writes JSON readable by the Guided Tour feature.
The JSON data is written to stdout and can be redirected to the file you will copy to Rundeck's user-asset directory.

The command's basic usage is shown below:

```
build-tour --source-dir <> [--name <> [--key <>]]
```

Example: Generate the JSON file for the "navigation" tour.

`build-tour --source-dir ./navigation > navigation-tour.json`

You can give the tour a more descriptive name using the --name <> option.

`build-tour --source-dir ./navigation --name "Learn Navigation"`

## JSON Format
The `build-tour` command generates the required JSON data structure. 

```json
{
  "name": "My tour display name",
  "key": "mytour-ID",
  "steps": [
    {
      "title": "My first topic",
      "content": "Some text"
    },
    {
      "title": "My second topic",
      "content": "Some text"
    }
  ]
}    
```

## Tour content

The tour's source structure contains one or more markdown files. 
Each markdown file represents a step in a tour. 

### Step content


The `build-tour` command also can interpret the
topic from the filename using the syntax _{NN}_-_{topic}_.md (eg, 00-stepA.md).

The numeric prefix is a file naming convention to define the order of the tour steps. The tour files are sorted alphanumerically in ascending order.

```
<tour basedir>
├── 00-stepA.md
├── 01-stepB.md
└── 0N-stepN.md
```

To have better control over a step's topic name rather than rely on the markdown file naming convention use following comment style at the top of the file to specify the step's title. 

```html
<!--
#/ title: My Step Topic
-->
```

## Configuration

Enable serving the tour files from `$RDECK_BASE/user-assets` dir. This setting must be set to true.
In the rundeck-config.properties set the following property:

```
rundeck.gui.staticUserResources.enabled=true
```

Create manifest in file called `$RDECK_BASE/user-assets/tour-manifest.json`. The file contains an array of tour keys:

```json
[
"tour1",
"tourN"
]
```
The element values should correspond to the tour key IDs.



