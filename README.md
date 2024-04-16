## Assessments results on discrepancy of SBOM ecosystem and a fast check code

###  Background

As SBOM can be widely used in software software chain management, the capability and issues within SBOM ecosystem can influence the employment of users, thus accurately assessments of the current SBOM state is important. To this end, we have conducted a series of assessments on key characteristics in SBOM applications to reveal the potential discrepancies hindering usage.

### Questions

We asked 3 questions:
    **1. Compliance**: Do SBOM tools generate outputs that adhere to user requirements and standards?
    **2. Consistency**: Do SBOM tools maintain consistency in transforming the produced SBOM?
    **3. Accuracy**: How accurate are the SBOM produced by tools in reflecting the objective software?

Upon 9970 SBOM documents generated from 6 SBOM tools (sbom-tool, ort, syft, gh-sbom, cdxgen and scancode) in both SPDX and CycloneDX on 1162 GitHub repositories, we assess these questions. To evaluate accuracy, 100 repositories are annotated for benchmark, comprising 660 components and 4,000 data fields.

### Results

This table shows average results across all the 6 tools, results are all in **package** level. Note that in the results for information of software itself is quite poor, for instance, we have 89.59% repositories contain licenses while only a minority are identified.

| Attr.       | pkg_name | version | author | purl   | license | copyright |
| ----------- | -------- | ------- | ------ | ------ | ------- | --------- |
| Compliance  | 79.61%   | 74.99%  | 17.84% | 67.53% | 32.34%  | 14.17%    |
| Consistency | 18.44%   | 22.24%  | 0.11%  | 24.99% | 2.12%   | -         |
| Accuracy    | 25.81%   | 10.66%  | 4.94%  | -      | 10.66%  | -         |

The findings indicate that while SBOM tools 100% support mandatory standards requirements (including Doc.: specVersion, License, Namespace, Creator; Comp.: Name, Identifier, downloadLocation, verificationCode), their performance in user case support is at 49.37% and the consistency within these supported use cases is on average of 17.63% (as the table shows). Accuracy assessments reveal significant discrepancies, with accuracy rates of 8.62%, 25.81%, and 12.3% as in software metadata, identified denpendent components, and detailed component information, underscoring substantial areas for improvement within the SBOM ecosystem.

### Fast check on code

We provide a fast check code at [here](https://github.com/dw763j/SBOM-Assessments).

The code is written in Python, and the required packages are in `code/requirements.txt`. You can install the required packages by running the following command:

```bash
pip install -r requirements.txt
```

We provide a all-in-one script to run the code for assessing the consistency of SBOM tools in the transfrom application. Clone this repository, and you can run the code with following command:

```bash
python test-run.py
```

It contains the following steps:
1. Extracts required data fields of the SBOMs and reformat them into JSON files. 
2. Match the peer-to-peer information in different data fields of SBOMs.
3. Evaluate the paired information in the matched SBOMs with the evalutaion operation provided by the evaluta module.
4. Give some basic statistics and output the results in a format of CSV file.

The results of the `test-run.py` will be in the `results` folder.

We hope our findings can help promote the SBOM ecosystem, any questions or discussions are welcomed.