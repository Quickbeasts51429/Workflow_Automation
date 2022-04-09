# Automating Galaxy workflows using the command line

### A short guide to Planemo
 Following commands were executed in sequence to generate the histories mentioned in the below section: 
* `git clone https://github.com/usegalaxy-eu/workflow-automation-tutorial.git`
* `cd workflow-automation-tutorial`
* `ls`

* `python3 -m venv planemo`
* `. planemo/bin/activate`
* `pip install planemo`

* `planemo workflow_job_init tutorial.ga -o tutorial-init-job.yml`
* `cat tutorial-init-job.yml`
* `printf "hello\nworld" > dataset1.txt`
* `printf "hello\nuniverse!" > dataset2.txt`
* `ls`

* `planemo run tutorial.ga tutorial-init-job.yml --galaxy_url <SERVER_URL> --galaxy_user_key <YOUR_API_KEY> --history_name "Test Planemo WF with no_wait" --tags "planemo-tutorial" --no_wait`

* `planemo run <WORKFLOW ID> tutorial-init-job.yml --galaxy_url <SERVER_URL> --galaxy_user_key <YOUR_API_KEY> --history_name "Test Planemo WF with Planemo" --tags "planemo-tutorial" --no_wait`

* `planemo profile_create planemo-tutorial --galaxy_url <SERVER_URL> --galaxy_user_key <YOUR_API_KEY>`

* `planemo run <WORKFLOW ID> tutorial-init-job.yml --profile planemo-tutorial --history_name "Test Planemo WF with profile" --tags "planemo-tutorial"`

Following are the histories created as a result of above commands:
* [Test Planemo WF with no_wait](https://usegalaxy.eu/u/soumyajha9090/h/test-planemo-wf-with-nowait)
* [Test Planemo WF with profile](https://usegalaxy.eu/u/soumyajha9090/h/test-planemo-wf-with-profile)
---
### Automated runs of a workflow for SARS-CoV-2 lineage assignment
 Following commands were executed in sequence to generate the histories mentioned in the below section: 
* `cd ../pangolin`
* `ls`

* `planemo workflow_job_init vcf2lineage.ga -o vcf2lineage-job.yml`
* `cat vcf2lineage-job.yml`

> import sys
from glob import glob
from pathlib import Path
import yaml
job_file_path = sys.argv[1]
batch_directory = sys.argv[2]
with open(job_file_path) as f:
    job = yaml.load(f, Loader=yaml.CLoader)
vcf_paths = glob(f'{batch_directory}/*.vcf')
elements = [{'class': 'File', 'identifier': Path(vcf_path).stem, 'path': vcf_path} for vcf_path in vcf_paths]
job['Variant calls']['elements'] = elements
with open(job_file_path, 'w') as f:
    yaml.dump(job, f)`

* `planemo run vcf2lineage.ga vcf2lineage-job.yml --profile planemo-tutorial --history_name "vcf2lineage test"`
* `planemo workflow_job_init tutorial.ga -o vcf2lineage-job-template.yml`
* ` bash run_vcf2lineage.sh `



Following are the histories created as a result of above commands:
* [vcf2lineage test(Pangolin)](https://usegalaxy.eu/u/soumyajha9090/h/vcf2lineage-test)
* [CWL Target History](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history)
* [CWL Target History_1](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-1)
* [CWL Target History_2](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-2)
* [CWL Target History_3](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-3)
* [CWL Target History_4](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-4)
* [CWL Target History_5](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-5)
* [CWL Target History_6](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-6)
* [CWL Target History_7](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-7)
* [CWL Target History_8](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-8)
* [CWL Target History_9](https://usegalaxy.eu/u/soumyajha9090/h/cwl-target-history-9)



