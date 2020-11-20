## Managing Compute Resources

Managing compute resources effectively involves several main components:

**Compute instances**
A central component of managing compute resources involves the ability to spin up a Virtual Machine (VM), provision the correct resources for that VM, and then launch a notebook—which you can then use to control other components of your project, such as by calling out to a compute cluster.

**Compute clusters**
A _compute cluster_ is a specialized cluster of Virtual Machines used to train ML models at scale, adjusting elastically to the requirements. Compute clusters can also employ specialized GPU or CPU resources.

**Inference clusters**
_Inference clusters_, as the name suggests, are used to establish a production ML endpoint and serve out predictions. Like compute clusters, inference clusters are also groups of Virtual Machines—and like compute clusters, they too can scale up and down in response to demand, thus ensuring that your customers always have a good response time. Inference clusters can be configured to do monitoring and logging, and set up to ensure that the model is running 24/7.

**Attached compute**
_Attached compute_, or "unmanaged compute," allows you to do integration with third party services. Those third party services could be anything from your own VM to something like a data bricks cluster that does managed Spark. If you have experience with a tool from, say, a previous job, you can integrate that tool with Azure ML Studio and thus use that pre-existing skill in your pipeline.