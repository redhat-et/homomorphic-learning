# Homomorphic Learning

The repository is dedicated to Methodology study for Multi-Party Learning also known as homomorphic learning.

## What is Homomorphic Learning?

Sharing private data with third parties, whether it be cloud services or other companies, can be a complex process due to the various privacy regulations in place, such as GDPR and CCPA. It's important for businesses to comply with these regulations to avoid facing significant fines and damaging their reputation.

While traditional encryption methods can be effective in storing private data on the cloud, there is a potential security risk when it comes to performing computations on the encrypted data. Homomorphic encryption (HE) provides a solution to this problem by allowing businesses to securely share private data with third parties to perform computations on their behalf.

With HE, the cloud service or outsourcing company only has access to encrypted data and can perform computations on it without needing to decrypt it. The encrypted result is then returned to the owner, who can use their private key to decrypt it. HE allows for operations to be performed on encrypted data without revealing the secret key needed to decrypt it, meaning that the raw data remains secure throughout the process.

Overall, Homomorphic Learning/ Encyption provides a secure and efficient way for businesses to share private data with third parties and perform computations without compromising the privacy and security of the data.

## Project Goals

_Investigate the state of the art for homomorphic learning, both as a technique for privacy aware machine learning as well as the open source tooling ecosystem around it._

1. **Literature survey:** Perform a literature survey on homomorphic learning to understand the state of the art from an abstract technique perspective and create a md file which highlightes different articles/papers along with brief summary of each.
[Here](docs/homomorphic_learning.md) are the key takeaways and results from the Literature Survey and some [relevant reserach papers](docs/homomorphic_learning.md#references).

2. **Tooling survey:** Perform a tooling survey to understand the landscape of homomorphic learning tooling, with a particular focus on open source tooling. 

 * To get a better understanding of various schemes and there resources, please see this [document.](docs/homomorphic_learning.md).
 * To see introductory notebooks for the Open Source Python HE tools, checkout the notebooks [here.](notebooks/)

3. **Proof of concept use case:** Construct a demonstration of a basic homomorphic learning use case. As a part of the proof of concept, we tried performing Logistic Regression on a heart disease data set. You can find the notebook and the results [here.](notebooks/Logistic_regression.ipynb)
