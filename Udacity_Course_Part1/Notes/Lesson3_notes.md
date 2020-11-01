## Lesson Outline: Datastores and Datasets, Data Drift & Security
This lesson is all about managing data by using Datastores and Datasets. Here are the main topics we'll cover:

**Managing data.** We'll talk about some of the MLOps workflows that are enabled by managing data within the Azure ML studio platform.
**Working with Datasets.** Working with datasets is critical for sharing data and having a high performance pipeline that doesn't require copying the data back and forth.
**Dataset monitoring and data drift.** If you collect your data, train a model, and then you get some new customers, those new customers may not be the correct target for the model that you created previously—you may need to recreate the model to get a better fit. With Dataset monitoring, you can detect those changes.
**Using Datasets in notebooks.** We'll cover the workflow for using Datasets in notebook, and we'll show you how you can leverage the open Datasets that are available in Azure.
**Dealing with sensitive data.** One of the most important topics in ML is how to handle personally identifiable information and protect it using encryption.

## Dataset Monitor and Data Drift
A common problem is that you may train a model on some data and achieve a good fit—but then, over time, new data comes in and the model fits less and less well. This is called data drift. You can use Dataset monitor to address this problem. Essentially, the process is:

1. **Register a baseline Dataset.** This would be a Dataset that has a good fit with your model (commonly you would use the Dataset with which you trained the model).
2. **Register a target Dataset.** This might be your model input data that you are receiving over time.
3. **Check for a delta.** If there's a specified delta (i.e., a given magnitude of difference) between the baseline and target Datasets, the system will trigger an alert (such as an email) and/or some form of automatic, corrective action (such as re-training the model).

### Security Principles and Practices
To keep your data from being compromised, you'll want your system to follow some core security principles and practices. Let's briefly review some of the main ones:

**Authentication.** This is all about who can log in. You want to restrict access using the PoLP principle, so that people who don't need to log in can't log in.
**Authorization.** This is all about what a user can access once they have logged in. Again, you want to restrict access using the PoLP to make sure that users are only able to access, for example, the folders that they really need to be able to access. A user can only access what they need to access.
**Securing compute targets and data.** You want to lock down both physical access to the data storage and also online access (e.g., applying best practices, such as firewall rules, to lock down access to open ports).
**Network security.** This is all about protecting data from interception. Are you using a VPN to limit access to the network resources? And are you also encrypting the data over the network?
**Data encryption.** Data encryption itself encompasses both data at rest and in transit. Obviously, you want to use secure protocols to prevent others from accessing the data. But by making sure the data is encrypted at all times, you ensure that even if the data is somehow breached, it still cannot be used.

### Azure Encryption Services
To help you ensure your data is secure, Azure has several encryption services that that are deeply integrated with the platform:

**Increased control over keys and passwords**, making it much easier to implement security best practices as described above.
**The ability to create and import encryption keys in minutes**, which ensures that you're not having performance bottlenecks by using encryption.
**Applications have no direct access to encryption keys.** Each service only accesses what it needs, so that If a machine is compromised, this breach won't then open the door to a further attack on your system.
