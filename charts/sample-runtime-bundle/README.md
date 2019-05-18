# Java application

I needed to add some additional steps to https://community.alfresco.com/community/bpm/blog/2018/12/10/activiti-7-beta-building-and-deploying-a-custom-business-process.

When executing 'helm lint charts/sample-runtime-bundle' I received an error:

==> Linting sample-runtime-bundle
[ERROR] templates/: render error in "sample-runtime-bundle/templates/deployment.yaml": template: sample-runtime-bundle/templates/deployment.yaml:24:7: executing "sample-runtime-bundle/templates/deployment.yaml" at <include "common.registry-pull-secrets" .>: error calling include: template: no template "common.registry-pull-secrets" associated with template "gotpl"

I got the original runtime-bundle chart by cloning the Activiti helm gitlab repo, then copied this into my sample-runtime folder. I made the exact edits to Chart.yaml in the article, which was just to change the image.repository, image.tag and service.name properties. I also did not clear requirements.yaml, ignoring this instruction.

After receiving the error, I also copied over the common folder from the cloned repo so that it is a sister directory to sample-runtime-bundle. This did not fix the error. I did so with these 2 commands:

	helm repo add activiti-cloud-charts https://activiti.github.io/activiti-cloud-charts/
	helm dep build charts/sample-runtime-bundle

Then this command completed without error:

	helm lint charts/sample-runtime-bundle

I continued with the instructions.


