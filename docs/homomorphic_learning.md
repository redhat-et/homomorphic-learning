# Homomorphic Encryption

## Introduction

Sharing private data with third parties, such as cloud services or other companies, is a challenge due to privacy regulations such as [GDPR](https://gdpr-info.eu/) and [CCPA](https://oag.ca.gov/privacy/ccpa). Failure to comply with these regulations can lead to serious fines and damage business reputations. Traditional encryption method provides an efficient way to store private data on the cloud in an encrypted form. However, to perform computations on data encrypted with these methods, businesses need to decrypt the data on the cloud, which can lead to security problems.

Homomorphic encryption (HE) enables businesses to share private data with third parties to get computational service securely. With HE, the cloud service or the outsourcing company has access only to encrypted data and performs computations on it. These services then return the encrypted result to the owner who can decrypt it with the private key. The concept of HE indicates that operations can be performed on encrypted data without the need to share the secret key needed to decrypt the data with the cloud provider. If decryption is carried on the result of any operation, it will be same as if calculations were done on the raw data.

Suppose we consider data _x1_, _x2_, ..., _xf and we successfully encrypt them to be _Enc(x1)_, _Enc(x2)_, ..., _Enc(xf)_. The homomorphic encryption system will allow us to efficiently compute a ciphertext function that will encrypt _f(x1,x2,...,xf)_ for any computable function _f_. This was first investigated by [Rivest et al. (1978)](https://dl.acm.org/doi/pdf/10.1145/359340.359342)

![Homomorphic Encryption](assets/images/Homomorphic_enc.png)


## Types of Homomorphic Encryption

HE schemes are classified depending on the possible circuits they can evaluate on encrypted data, differences lie in the available gates to use, and the depths of those circuits. In other words, depending on the possible functions, _f_, you can compute and how many operations can be chained on a ciphertext, HE schemes can be classified into three main types:

- **Partially-HE (PHE)** : This type of scheme can evaluate any circuit composed of a single type of gate, addition or multiplication, but never both. It doesn’t restrict neither the size nor depth of the circuit. This type is well suited for the applications that only need to perform either addition or multiplication on encrypted data. The RSA cryptosystem is an example of a PHE that allows an unbounded number of modular multiplications.

- **Somewhat-HE (SHE)** : This type of scheme can evaluate circuits composed of addition and multiplication gates, but with the restriction on the depth. SHE is useful for evaluating low degree polynomials up to some level, however we sometimes need to evaluate circuits of arbitrary depth.

- **Fully-HE (FHE)** :A concept first conceived by [Rivest et al. (1978)](https://dl.acm.org/doi/pdf/10.1145/359340.359342) but it remained unrealized until Craig Gentry presented a [first feasible FHE scheme in 2009](https://www.cs.cmu.edu/~odonnell/hits09/gentry-homomorphic-encryption.pdf). This encryption scheme can evaluate circuits composed of both addition and multiplication gates. In contrast to SHE, FHE has unlimited circuit depths which makes It suitable for deep learning applications. Although many FHE schemes have been proposed during the last decade, it has been difficult to use them in practice. In the linked paper, Craig built FHE on top of SHE by using what he called bootstrapping. Although FHE being the most powerful type, in order to put such a scheme into practice, one needs to consider other factors as well like the cost of evaluation, size of ciphertext, domain of plain text (integer or real numbers), and the cost of bootstrapping. FHE has gone from theoretical breakthrough to practical deployment, dropping the initial 30 minutes required to compute the multiplication between two encrypted values down to less than 20 milliseconds. Even then, FHE multiplication is still around seven orders of magnitude slower than native CPU integer multiplication instructions.

## HE Schemes

As mentioned earlier, there are various types of HE but there are various HE scemes that can also be categorized into the partial and fully homomorphic. Here are some schemes that are widely known :

* Pallier
* CKKS
* BFV
* GSW
* BGV

## Applications

Homomorphic Encryption has various advantages and can be applied to application starting from education and healthcare to smart electric grids and MLaaS (Machine Learning as a service). Basically it can be applied to anywhere where the input data privacy is the most important thing. Anyway the data usage is super complex due to the regulations, privacy concerns and the vitality of the data. Industries and sectors working with non-intrusive and privacy conserving security - detection of secturing breaches etc. Thanks to encryption, all these opertaions, parameters are kept private but often not easily reversible.

// Add diagram or MLaaS

Craig Gentry mentioned in his [thesis](https://crypto.stanford.edu/craig/craig-thesis.pdf) that Full Homomorphic encryption has numerous applications. For example, it enables private queries to a search engine - the user submits an encrypted query and the search engine computes a succinct encrypted answer without ever looking at the query in the clear. It also enables searching an encrypted data - a user stores encrypted files on a remote file server and can later have the server retrieve only files that, when decrypted, satisfy the Boolean constraint, even though the server cannot decrypt the files on its own. More broadly, FHE improves the efficiency of secure multi party computation.

Researchers have already identified several practical applications of FHE, some of which are discussed below:

* **Security Data Stored in the Cloud :** Using homomorphic encryption, you can secure the data that you stored in the cloud while also retaining the ability to calculate and search ciphered information that you can later decrypt without compromising the integrity of the data as a whole.

* **Enabling Data Analytics in Regulated Industries :** HE allows data to be encrypted and outsourced to commercial cloud environments for research and data sharing purposes while protecting user or patient data privacy. It can be used for businesses and organizations across a variety of industries including financial services, retail, information technology, and healthcare to allow people to use data without seeing its unencrypted values. Examples include [predictive analysis for medical data](https://www.sciencedirect.com/science/article/pii/S1532046414000884) without putting data privacy at risk, [preserving customer privacy](https://eprint.iacr.org/2015/1192.pdf) in personalized advertising, financial privacy for functions like [stock price prediction algorithms](https://eprint.iacr.org/2015/1192.pdf), and forensic image recognition.

* **Improving Election Security and Transparency :** Researchers are working on [how to use homomorphic encryption to make democratic elections more secure and transparent](https://ieeexplore.ieee.org/document/7492759). For example, the [Paillier encryption](https://www.researchgate.net/profile/Pascal-Paillier/publication/249581677_Paillier_Encryption_and_Signature_Schemes/links/56b35be308ae156bc5fb1f1c/Paillier-Encryption-and-Signature-Schemes.pdf) scheme, which uses additionoperations, would be best suited for voting-related applications because it allows users to add up various values in an unbaised way while keeping their values private. This technology could not only protect data from manipulation, it could allow it to be independently verified by authorized third parties.

## Existing Tools, Libraries and Research

Technological companies, (like Microsoft, Google), have initiated programs to advance homomorphic encryption to make it more universally available and user friendly. Microsoft, has created [SEAL](https://www.microsoft.com/en-us/research/project/microsoft-seal/) (Simply Encrypted Arithmatic Library), a set of encryption libraries that allow computations to be performed directly on encrypted data. Companies can use [SEAL](https://github.com/microsoft/SEAL) to create platforms to perform data analytics on information while it's still encrypted and the owners of the data never have to share their encryption keys to anyone else. Google, with its [open-source cryptographic tool](https://github.com/google/private-join-and-compute), Private Join and Compute, is focussed on analyzing data in its encrypted form, with only the insights derived from the analysis visible, and not the underlying data itself.

Efficient implementations of FHE are mostly written in high performance languages like C++, posing a high entry barrier to novice users. However, for most data science and machine learning applications, Python is a standard language. This can be achieved with the implementation of Python wrapper function. [Pyfhel](https://dl.acm.org/doi/pdf/10.1145/3474366.3486923) provides a Python wrapper for the [Microsoft Seal](https://github.com/microsoft/SEAL) library, extendable to other C++ libraries, that goes beyond merely exposing the underlying API by adding a carefully designed abstraction layer that feels at home in Python. Pyfhel offers:

* One-click installation, including the underlying libraries.
* A high-level Python first abstraction layer that makes working with FHE significantly easier. 
* High-level API's for low level functionalities not generally exposed.

In additon to Pyfhel, their exists a plethora of Python wrappers for FHE libraries. Most rely on automatic C++ wrapping tools like [_pybind11_](https://pybind11.readthedocs.io/en/stable/) or Boost.

* [Python-paillier](https://github.com/data61/python-paillier) open-source implementation in python of the Paillier scheme.
* [_PySEAL_](https://arxiv.org/abs/1803.01891) is no-longer maintained pybind11-based wrapper. Many require the user to compile underlying libraries themselves, using the Unix-only toolchain, like more recent [SEAL-Python](https://github.com/Huelse/SEAL-Python).
* [TenSEAL](https://arxiv.org/abs/2104.03152) which appeared several years after the initial release of Pyfhel shows the most promise. It is pybind11 based and features a one-click setup, but focussed mostly on high level Machine Learning and Tensor operations.
* [PySyft](https://github.com/OpenMined/PySyft) is OpenMined's open source stack that provides secure and private Data Science in Python. Syft decouples private data from model training, using techniques like Federated Learning, Differential Privacy, and Encrypted Computation. This is done with a numpy-like interface and integration with Deep Learning frameworks, so that you as a Data Scientist can maintain your current workflow while using these new privacy-enhancing techniques.
* Other approaches (e.g., [pyFHE](https://dspace.mit.edu/handle/1721.1/129204)) implement schemes directly in Python, at the cost of significantly slower operations.

A curated list of amazing homomorphic encryption libraries, software and resources can be found [here](https://github.com/jonaschn/awesome-he).

We will be performing a comparative study between these opensource python tools and libraries and based on these results, we will create a proof of concept use case that demonstrates a basic homomorphic learning example.

## Federated Learning

Similar to Homomorphic Learning, Federated Learning caters to the problem of not being able to centralize the training data due to data privacy, secrecy, regulatory compliance and heavy volume and loads of data.

### IBM Federated Learning

[IBM Federated Learning](https://ibmfl.mybluemix.net/introduction) supports multiple machine learning models out-of-the-box, including:

* Models written in Keras, PyTorch and TensorFlow
* Linear classifiers/regressions (with regularizer): logistic regression, linear SVM, ridge regression and more
* Decision Tree ID3
* Deep Reinforcement Learning algorithms including DQN, DDPG, PPO and more
* Naïve Bayes

IBM FL is part of Watson Studio and is available as a service on the cloud here, and you may also use it as part of your Cloud Pak for Data installation. The community edition is a stand-alone library that is suited for academic users, researchers, not for production or commercial use. We will be trying this out as well as a part of tool-evaluation study.

## Limitations and Conclusions

Homomorphic encryption is a very exciting subject with a tremendous potential to disrupt the landscape of online privacy and AI evolution. The urgent need for such a solution is apparant and some of the first use cases has been implemented. Between slow computation speed or accuracy problems, FHE remains commercially infeasible for computationally-heavy applications. There is certainly much progress to be made and many more to come just around the corner. 

Besides being computationally expensive Homomorphic encryption limits the set of operations one can perform on the data. For instance operations like division, inverse multiplication etc are not feasible either. 

## References

1. [A brief history on Homomorphic learning: A privacy-focused approach to machine learning](https://arxiv.org/pdf/2009.04587.pdf)
2. [https://paperswithcode.com/paper/fully-homomorphically-encrypted-deep-learning](https://paperswithcode.com/paper/fully-homomorphically-encrypted-deep-learning)
3. [https://towardsdatascience.com/homomorphic-encryption-intro-part-1-overview-and-use-cases-a601adcff06c](https://towardsdatascience.com/homomorphic-encryption-intro-part-1-overview-and-use-cases-a601adcff06c)
4. [Automated Exploration of Homomorphic Encryption Scheme Input Parameters](https://pdf.sciencedirectassets.com/287016/1-s2.0-S2214212620X00056/1-s2.0-S2214212620307912/am.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEAsaCXVzLWVhc3QtMSJHMEUCIQDVcn4UMm%2BYZL4W5Xe8CrtMyEIJMrECxA6FitEKLgfj3gIgFpln7b3FcRCyHJnek65ro9vqCMhiAjl3cizQvNrNPxwq0gQIRBAEGgwwNTkwMDM1NDY4NjUiDNuuBStteWKhAvrW9SqvBLyqMpHvunuBGnzjvd5PvPGxI81er9%2BKqIKfmeKewX5AUU7a4pIlkmBdLVJwjObcOeuoSMV96mUTjWd78Tosqt%2FwHBOnaxe%2BkYtaslLKVa1yQEWSmUGtOUpCAhdvC2K6wwDqgSNdMil2DNbP0sDuDJyvnOzye%2FAYLgsxu7n90L%2BCVZ31HkSfoAlP%2BWiL303yE6RbDK6ph%2BJ0W%2FxX26KR3Sx3zVonyX%2BF0N9p5Hb2w0RXdCLrjxRevyu7AcmQDCi4gHJUJlk8yT%2FIRMD%2BdEBXEtzMSLEDqmXcWpLfSkpD%2B%2FwQ06ESjlFmBHGAc0Mlh0NuJzZDsMm%2BBePZqUSm%2BQU52lD28f9pipGpHFhlGmRP8ljTmPH44NU%2FlvlzGZHoL4AAMHsFK2EZXZzE0Pyrb6BG1YxudSgLj3a6UqgkZ4gsXKbHismXNoUmfdcOTEA8LbEkTVU6XNgFhQcST3Q85Y%2ByXFNdUE8VfTx7tB3Fy4XAxuxkpI8LDg2sunOOx2ZhzL2wfoLGdRlIPIpnVReo14ehgrPnzJPFMbpiGLB0CKxBlyMzS%2BCgJY2MwNPTLaEnlIYSTnA8l%2FV7facoREWpinzevPeH0ge7gisdm6wNr%2BfCMaEUE0O1lpuqDojY83WRDe0Eprm28CJpihkL7RIXsne%2Bonvfm57lP%2B5HLtkSYEi0a0H8B0w1wL6get1Xm3gsJLjZNaxxCAoo04EkTNR8X3rrc2Ma125vMu2ts8vCemTPfTow%2Bv2vlgY6qQHu%2BKYZ6ujQN0fR%2FGJhyMeiRBbYDCnzWxCVvFeqz%2Beo9jr3s%2BvinfYwYxxYSN9lHzgD%2FNvBlFxUzCcIiqV%2FKoN4bNIJGRnfypswcJqKUdlPtnORXgJX%2Fk9dui4PO4kbBLy8l86QEGfP1N0tdQYr6i2UTvPhCWqvXMkHHYS9woM2fxErOUd8yRRCwTtsPlp%2FbCCukkQQSDbY%2Bz5ImEjepVtdA7X2JHFiALOp&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220711T120019Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYTZAHPRBZ%2F20220711%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=a35660880795e45f9174dfa0f95411b873b3d42984321ff363e29c93bec11833&hash=6bf2f6d62557f418804f5cd557c09a783b24aa8b06300f8e1c5687e1092e2278&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S2214212620307912&tid=pdf-7034a620-39a7-4d7c-b6f3-09781bfdd2fd&sid=f414b94a6ef3a0423a0b419-f7daedefc7begxrqa&type=client)
5. [https://avalonlibrary.net/ebooks/David%20Kahn%20-%20The%20Codebreakers.pdf](https://avalonlibrary.net/ebooks/David%20Kahn%20-%20The%20Codebreakers.pdf)
6. [Multiparty Homomorphic Encryption](https://courses.csail.mit.edu/6.857/2016/files/17.pdf)
7. [Systematic Review on Fully Homomorphic Encryption Scheme and Its Application | SpringerLink](https://link.springer.com/chapter/10.1007/978-3-030-47411-9_29)
8. [Privacy Preserving Multi-party Machine Learning with Homomorphic Encryption](https://inspire.cse.unt.edu/sites/default/files/17.pdf)
9. [Homomorphic Encryption and Federated Learning based Privacy-Preserving CNN Training: COVID-19 Detection Use-Case](https://arxiv.org/abs/2204.07752)
10. [Fully Homomorphic Encryption Using Ideal Lattices](https://www.cs.cmu.edu/~odonnell/hits09/gentry-homomorphic-encryption.pdf)
11. [Federated Learning by IBM](https://ibmfl.mybluemix.net/introduction)
