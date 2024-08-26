# PLASO Installation and Testing

PLASO is a popular digital forensic tool used to extract and analyze temporal events from various data sources.

## Installation of Docker

To begin, you'll need Docker installed on your system. Docker is a containerization platform that allows you to run applications in isolated environments.

-Installation Guide: [Docker Installation Instructions](https://docs.docker.com/get-docker)


## Pulling the PLASO Docker Image
Once Docker is set up, the next step is to pull the PLASO Docker image. This simplifies installation and avoids potential issues with dependencies on macOS.

**Command**: 
```bash
docker pull log2timeline/plaso
 ```
By pulling the 'log2timeline/plaso' Docker image, you ensure that the latest version of PLASO and its dependencies are downloaded.

<img width="566" alt="Screenshot 2024-08-26 alle 15 22 18" src="https://github.com/user-attachments/assets/d923d3c4-13e4-452f-8a01-2c8a9a536390">



## Verifying the PLASO Installation

After pulling the image, verify that PLASO is installed correctly by checking its version.

**Command**:  
```bash
docker run log2timeline/plaso log2timeline.py --version
 ```


![image](https://github.com/user-attachments/assets/3a8f87dd-76da-4319-9b42-df05add9998c)


## Creating a Testing Environment

To test PLASO, create a small file structure for it to analyze.

**Commands**: 
 ```bash
mkdir ~/plaso_test
cd ~/plaso_test
echo "This is a test file." > file1.txt
mkdir test_folder
echo "Another test file." > test_folder/file2.txt
 ```


**Outcome**: The directory structure should look like this:
 ```bash
  ~/plaso_test/
  ├── file1.txt
  └── test_folder/
      └── file2.txt
 ```

<img width="571" alt="Screenshot 2024-08-26 alle 15 29 18" src="https://github.com/user-attachments/assets/a02f610a-df80-47a6-b29b-ea01f09ee6ed">



---

## Running PLASO to Create the Timeline

Use PLASO to generate a timeline from the test data.

- **Command**:
  ```bash
  docker run --rm -v ~/plaso_test:/evidence log2timeline/plaso log2timeline.py /evidence/output.plaso /evidence
  ```

- **Explanation**:
  - **`--rm`**: Automatically removes the container after the command finishes, keeping the system clean.
  - **`-v ~/plaso_test:/evidence`**: Mounts the local directory (`plaso_test`) into the container at `/evidence`, making it accessible to PLASO.
  - **`log2timeline.py /evidence/output.plaso /evidence`**: Specifies that the timeline output should be saved to `/evidence/output.plaso`, analyzing everything in the `/evidence` directory.

<img width="567" alt="Screenshot 2024-08-26 alle 15 35 57" src="https://github.com/user-attachments/assets/c5eb86a9-00fb-4d93-8db9-743fb577145c">




---

## Extracting and Viewing the Timeline

After generating the timeline, extract and view the events using `psort.py`.

- **Command**:
  ```bash
  docker run --rm -v ~/plaso_test:/evidence log2timeline/plaso psort.py -o dynamic /evidence/output.plaso > ~/plaso_test/timeline.txt
  ```

- **Explanation**:
  - **`-o dynamic`**: Specifies a dynamic output format, which adjusts to the available fields.
  - **`> ~/plaso_test/timeline.txt`**: Redirects the output to a text file.

<img width="565" alt="Screenshot 2024-08-26 alle 15 36 49" src="https://github.com/user-attachments/assets/1e6327ad-f499-4bc8-86ac-310db0dd42e2">



--- 

  






