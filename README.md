# my-genivi-pipelines

[Jenkins Pipelines](https://jenkins.io/doc/book/pipeline/) for building [GENIVI Open Source Projects](http://projects.genivi.org/).

### System Requirements

* [Jenkins v2.32](https://jenkins.io/) or greater with the following installed plugins:
  - [Blue Ocean Plugin v1.0.0-b23](https://wiki.jenkins-ci.org/display/JENKINS/Blue+Ocean+Plugin)
  - [Pipeline Multibranch Plugin v2.12](https://wiki.jenkins-ci.org/display/JENKINS/Pipeline+Multibranch+Plugin)
  - **NOTE**: You may use [easy-jenkins](https://github.com/gmacario/easy-jenkins) to install all the prerequisites
* Lot of time, network bandwidth and disk space...

### Usage

From the Jenkins dashboard, click **New Item**

* Enter an item name: `my-genivi-pipelines`
* Type: **Multibranch Pipeline**

then click **OK**. Inside the project configuration page, add the following information:

* Branch Sources > Add source > Git
  - Project Repository: `https://github.com/gmacario/my-genivi-pipelines`

then click **Save**.

Select job "my-genivi-pipelines", then click **Build Now**.

Click on **Blue Ocean** to display the Blue Ocean Dashboard.

### License and Copyright

This project is licensed under the MIT License - for details please see the [LICENSE](LICENSE) file.

Copyright (C) 2017, [Gianpaolo Macario](https://gmacario.github.io/)
