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

## Applications

Craig Gentry mentioned in his [thesis](https://crypto.stanford.edu/craig/craig-thesis.pdf) that Full Homomorphic encryption has numerous applications. For example, it enables private queries to a search engine - the user submits an encrypted query and the search engine computes a succinct encrypted answer without ever looking at the query in the clear. It also enables searching an encrypted data - a user stores encrypted files on a remote file server and can later have the server retrieve only files that, when decrypted, satisfy the Boolean constraint, even though the server cannot decrypt the files on its own. More broadly, FHE improves the efficiency of secure multi party computation.

Researchers have already identified several practical applications of FHE, some of which are discussed below:

* **Security Data Stored in the Cloud :** Using homomorphic encryption, you can secure the data that you stored in the cloud while also retaining the ability to calculate and search ciphered information that you can later decrypt without compromising the integrity of the data as a whole.

* **Enabling Data Analytics in Regulated Industries :** HE allows data to be encrypted and outsourced to commercial cloud environments for research and data sharing purposes while protecting user or patient data privacy. It can be used for businesses and organizations across a variety of industries including financial services, retail, information technology, and healthcare to allow people to use data without seeing its unencrypted values. Examples include [predictive analysis for medical data](https://www.sciencedirect.com/science/article/pii/S1532046414000884) without putting data privacy at risk, [preserving customer privacy](https://eprint.iacr.org/2015/1192.pdf) in personalized advertising, financial privacy for functions like [stock price prediction algorithms](https://eprint.iacr.org/2015/1192.pdf), and forensic image recognition.

* **Improving Election Security and Transparency :** Researchers are working on [how to use homomorphic encryption to make democratic elections more secure and transparent](https://ieeexplore.ieee.org/document/7492759). For example, the [Paillier encryption](https://www.researchgate.net/profile/Pascal-Paillier/publication/249581677_Paillier_Encryption_and_Signature_Schemes/links/56b35be308ae156bc5fb1f1c/Paillier-Encryption-and-Signature-Schemes.pdf) scheme, which uses additionoperations, would be best suited for voting-related applications because it allows users to add up various values in an unbaised way while keeping their values private. This technology could not only protect data from manipulation, it could allow it to be independently verified by authorized third parties. 

## Existing Tools and Research

Technological companies, (like Microsoft, Google), have initiated programs to advance homomorphic encryption to make it more universally available and user friendly. Microsoft, has created [SEAL](https://www.microsoft.com/en-us/research/project/microsoft-seal/) (Simply Encrypted Arithmatic Library), a set of encryption libraries that allow computations to be performed directly on encrypted data. Companies can use [SEAL](https://github.com/microsoft/SEAL) to create platforms to perform data analytics on information while it's still encrypted and the owners of the data never have to share their encryption keys to anyone else. Google, with its [open-source cryptographic tool](https://github.com/google/private-join-and-compute), Private Join and Compute, is focussed on analyzing data in its encrypted form, with only the insights derived from the analysis visible, and not the underlying data itself.

Efficient implementations of FHE are mostly written in high performance languages like C++, posing a high entry barrier to novice users. However, for most data science and machine learning applications, Python is a standard language. This can be achieved with the implementation of Python wrapper function. [Pyfhel](https://dl.acm.org/doi/pdf/10.1145/3474366.3486923) provides a Python wrapper for the [Microsoft Seal](https://github.com/microsoft/SEAL) library, extendable to other C++ libraries, that goes beyond merely exposing the underlying API by adding a carefully designed abstraction layer that feels at home in Python. Pyfhel offers:

* One-click installation, including the underlying libraries.
* A high-level Python first abstraction layer that makes working with FHE significantly easier.
* High-level API's for low level functionalities not generally exposed.

In additon to Pyfhel, their exists a plethora of Python wrappers for FHE libraries. Most rely on automatic C++ wrapping tools like [_pybind11_](https://pybind11.readthedocs.io/en/stable/) or Boost. [_PySEAL_](https://arxiv.org/abs/1803.01891) is no-longer maintained pybind11-based wrapper. Many require the user to compile underlying libraries themselves, using the Unix-only toolchain, like more recent [SEAL-Python](https://github.com/Huelse/SEAL-Python). [TenSEAL](https://arxiv.org/abs/2104.03152) which appeared several years after the initial release of Pyfhel shows the most promise. It is pybind11 based and features a one-click setup, but focussed mostly on high level Machine Learning and Tensor operations. Other approaches (e.g., [pyFHE](https://dspace.mit.edu/handle/1721.1/129204)) implement schemes directly in Python, at the cost of significantly slower operations.

A curated list of amazing homomorphic encryption libraries, software and resources can be found [here](https://github.com/jonaschn/awesome-he). 


## Limimtations and Conclusions

Homomorphic encryption is a very exciting subject with a tremendous potential to disrupt the landscape of online privacy and AI evolution. The urgent need for such a solution is apparant and some of the first use cases has been implemented. Between slow computation speed or accuracy problems, FHE remains commercially infeasible for computationally-heavy applications. There is certainly much progress to be made and many more to come just around the corner. 