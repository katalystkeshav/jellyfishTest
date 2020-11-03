
1. Create a simple, yet resilient application, which responds to HTTP requests.

I will create a simple http application in golang.

2. The application should allow for individual node failures, without impacting availability.

Created Auto Scaling group which will take care of the high availability of the app.

3. The application should be able to scale based on load.

Applied target tracking policy which will increase the no of instances when avg cpu load increases.

4. Underlying cloud infrastructure should be defined as code, stored in a repository, with instructions about how it should be built.

I have used CloudFormation to create the whole infrastructure.
Steps -
You need to create a S3 bucket and then place all this code inside that bucket.
You can change the parametes as per your requirements.
After uploading all the files in S3 bucket, please replace the url with your S3 bucket's url in main file.
Create a new CloudFormation stack and provide the url of main file.
All of the resources mentioned in main file will be created

5. Changes to code should result in the triggering of a simple continuous integration test.

A CodeCommit repo is also created in the stack and we can store our code in that repo. 
I will create CodePipeline which will contain CodeBuild which will be used to build and test the code and the artifacts will be stored in S3 bucket.
After this CodeDeploy will take the code and then deploy it on the instances present in out Auto Scaling group.
Any push made in our repo will start this CodePipeline.

6. A successful CI test should trigger an automated deployment.

Already ecplained in point no 5.

7. Implement a simple degree of monitoring & logging.

For logging we can use filebeat with ElasticSearch or fluentd with S3 depending on our requirement.
For simple monitoring solution we can install CloudWatch agent on our EC2 instance and create an ami otherwise for more complex solution we can use Prometheus.