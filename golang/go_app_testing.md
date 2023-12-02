### Different Tests of APP
- What is stress testing and load testing when did you use them?
    - load testing to see how a app reacts/behaves when on expected load.
    - stress testing is to find the limits or breaking points of the app i.e above the expected load.

- What is a scenario in which you performed stress testing? 
    - We have a setup where clients publish their documents to multiple sites.
    - some clients/orgs do came up with a use case where they want to increase their sites.
    - Its not a straight forward decision to just increase the number of sites. As that would affect the systems and eventually have blast radius as most of the infrastructure is multitenant. 
    - As I know the biggest traffic is when a document is circulated to multiple sites at a time. 
    - I stress tested the circulation workflow with 100, 200, 300, 400, 500 sites
    - systems can handle circulations upto 300 sites without any latency changes. But from 300 there is a steady increase in latency. Which suggested that the limit of stress test is at 300 sites. 
    - there is a decision where we can approve 300 sites or any number of sites but limit the circulation of a document to at most 300 sites.

- How would you determine the appropriate load level for load testing scenario?
    - By existing patterns of usage [ this can be achieved by looking at the existing metrics ]
    - By iteratively increaring the load
    - define performance goals: latency, error thresholds, CPU and Memory Usage [ for scaling infra if necessary ]
    - monitor metrics for any anomalies in defined performance goals under load. 

- How did you perform load testing on your application, can you give an example?
    - I used locust for performaing load and stress testing in my app.
    - we could dynamically adjust the load using locust. 
    - example of locust script: 
        ```python
            from locust import HttpUser, task, between 
            
            class DocumentUser(HttpUser):

                wait_time = between(1,3)
                host = f"http://yourdomain/api"

                @task
                def create_circulations(self):
                    document_info = {"document_id": id, "document_headline": headline, "target_sites": self.generate_randomPtarget_sites()}
                    response = self.client.post('/circulate-document', json=document_info)

                    if response.statsu_code == 200:
                        pass
                    else        
                        self.log_failure("circulation document failed")                

                def generate_random_target_sites(self):
                    # Generate a random number of target sites for each user
                    num_target_sites = random.randint(1, 10)  # Adjust the range as needed
                    return ["Site{}".format(i) for i in range(1, num_target_sites + 1)]
                        
                    
        ```

 