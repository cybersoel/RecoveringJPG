# Recovering a JPG file from a RAM dump

## Key Learnings and Skills Demonstrated

- **Digital Forensics**: Showcased practical skills in memory forensics and file recovery techniques.
- **Hex Editing**: Demonstrated proficiency in using hex editors to analyze and manipulate binary data.
- **File Signatures**: Applied knowledge of file signatures (magic numbers) to identify JPG files within raw data.
- **Memory Dump Analysis**: Exhibited understanding of RAM structure and the process of analyzing memory dumps.
- **Data Carving**: Implemented manual data carving techniques to extract specific file types from unstructured data.
- **Forensic Tool Usage**: Utilized FTK Imager, demonstrating familiarity with professional forensic tools.
- **File System Knowledge**: Displayed understanding of how files are stored and represented in computer memory.
- **Binary Data Interpretation**: Demonstrated ability to interpret binary data and identify relevant structures.
- **Metadata Analysis**: Leveraged file metadata to assist in the location and recovery of target files.
- **Search Techniques**: Employed various search methods to locate specific data within large datasets.
- **Data Extraction**: Successfully extracted and reconstructed a JPG file from raw memory data.
- **Documentation Skills**: Created a clear, step-by-step guide for the file recovery process.
- **Problem-Solving**: Approached a complex task methodically, breaking it down into manageable steps.
- **Cybersecurity Awareness**: Highlighted the persistence of data in computer memory, relevant to security and privacy concerns.
- **Ethical Considerations**: Conducted the exercise within an educational context, emphasizing the importance of ethical use of forensic techniques.

This project simulates a real-world digital forensics scenario, providing hands-on experience with memory analysis and file recovery. The skills demonstrated are directly applicable to roles in digital forensics, incident response, and cybersecurity investigation. It showcases the ability to recover potentially crucial evidence from volatile memory, a key skill in many cybersecurity and law enforcement contexts.


<h1 align="center">Summary Diagram</h1>


<p align="center">
<br/>
<img width="830" alt="Portfolio" src="https://i.imgur.com/2eWQTSQ.png">
<br />
</p>


<br />
<br />

<h1 align="center">Project walk-through</h1>

<br />
<br />

---
<a name="toc"></a>
**Table of Contents:**

- [Introduction](#introduction)
- [Preparation](#preparation)
- [Step-by-Step Process](#sbsp)



---

<h4>Tip: Any configuration options not mentioned in the walkthrough can be left at their default settings</h4>

---

[back to top](#toc)
## Introduction

In this lab, our goal is to extract and recover a JPG file from a memory dump without using special carving tools.

<br />

Keep in mind that RAM is dynamic and volatile, with data constantly being written, read, and rearranged. If your JPG file is too large, the data may become fragmented and scattered throughout the RAM, making recovery difficult using a simple hex editor. In such cases, specialized forensic carving tools may be necessary.

<br />

To improve your chances of success, select a JPG/JPEG file that is as small as possible. You can reduce the image size using tools like Photoshop or free online platforms like Photopea. Go to [File] > [Export as JPG], then adjust the pixel dimensions (Width/Height) to reduce the file size. Ideally, a JPG file smaller than 1KB will almost guarantee a successful recovery.


<br />
<br />

---

[back to top](#toc)
## Preparation

<br />
<br />

 - You will need a target JPG or JPEG file for retrieving.
 - FTK Imager (The is a free tool you can download online. You might need to register an account to get the download link via email)
     - Alternatively, you can use free tools like Dumpit, Belkasoft Live RAM Capturer, and Magnet Forensics RAM capture
 - RAM dump file (You need to use one of the above tools to capture your RAM. Please search how to capture RAM from online or youtube.)
     - There are few ways to make this JPG file retrievable later. Make sure to do one of the followings:
         - Open the JPG file: The simplest method is to open the JPG file in an image viewer or editor shortly before performing the RAM dump.
         - Copy the file: Perform a copy operation of the JPG file just before the RAM dump. This action will likely cache the file in RAM
         - Use a file explorer: Navigate to the folder containing the JPG file using File Explorer. This might cache thumbnail data and file metadata in RAM.
         - Edit the image: Open the JPG in an image editing software and make some minor edits. This will ensure the file data is in RAM and might create additional temporary data
         - Print or print preview: Initiate a print job or open a print preview of the JPG. This typically loads the full image into RAM.
         - Create a slideshow: We can create a quick slideshow using the built-in Photos app, including our target JPG.
         - Perform file operations: Rename, move, or change attributes of JPG file. These operations might cause parts of the file to be cached in RAM.
     - However, in this lab, I recommend simply opening the JPG file before dumping the RAM.       
 - Hex Editor (You can use something like HxD Hex editor or just use FTK Imager as it has a built-in hex editing tool)


<br />
<br />
<br />
<br />


---
<a name="sbsp"></a>
[back to top](#toc)
## Step-by-Step Process



 - I am going to retrieve this .jpg file.
<p align="center">
<br/>
<img width="450" alt="Portfolio" src="https://i.imgur.com/0wNNrxJ.png">
<br />
<br />
<br />
<br />



 - This is the RAM dump file I am going to use. Like I mentioned above, try to prepare a very small size jpg file. Open the file so your RAM can load the file, then capture your RAM using one of the tools mentioned above. 
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/mYx1NNP.png">
<br />
<br />
<br />
<br />


 - Open the memory file with a hex editor. I am using FTK imager. Select [File] > [Add Evidence Item]
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/3Ki1mB7.png">
<br />
<br />
<br />
<br />


 - Select [Content of a Folder]
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/HRghks1.png">
<br />
<br />
<br />
<br />

 - Choose the folder that contains your RAM file.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/0cmDGdV.png">
<br />
<br />
<br />
<br />

 - Right-click and pick [Fit to window] to see more information.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/g701eQd.png">
<br />
<br />
<br />
<br />


 - First thing we have to do is find out the standard jpg header (aka magic numbers/file signature: the first few bytes of a file that are unique to a particular file type) and also the footer (trailer). We can simply search the information from the internet.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/WmDGPil.png">
<br />
<br />
<br />
<br />


 - Header always starts with FF D8 FF. (However, most JPG/JPEG file starts with FF D8 FF E0)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/1XF21ef.png">
<br />
<br />
<br />
<br />


 - You can also check ntfs.com/jpeg-signature-format.htm
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/S7zRfBw.png">
<br />
<br />
<br />
<br />

 - Footer ends with FF D9
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/lBE5qCA.png">
<br />
<br />
<br />
<br />

 - We need to find a file that starts with "FF D8 FF" and ends with "FF D9". Press Ctrl + F and type the file header
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/eSVeg3O.png">
<br />
<br />
<br />
<br />

It's going to take quite a long time to manually inspect since the memory file is typically couple GB. Typically we can use file carving tools like PhotoRec, Foremost, or Scalpel, instead of using a basic hex editor.

<br />

There are couple ways to accelerate the searching process:

<br />

Perform a string search for the filename, parts of the filename, or the file metadata. This might lead us to file table entries pointing the JPG data.
Let's use file's meta data as a reference and use Ctrl + F (find: text string) to find the file directly. We still need the file header and footer (FF D8 FF, FF D9) to find the beginning and the end of the file.


<br />
<br />
<br />
<br />


 - My file was found between 350F70000 ~ 350F7242A (Offset)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/z3Zjzf7.png">
<br />
<br />
<br />
<br />

 - As you can see, the file starts with FF D8 FF E0 and ends with FF D9
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/4Tz0ble.png">
<br />
<br />
<br />
<br />

 - Select from the header to the footer and click [Save selection] (In other hex editor tools, you can just copy and paste to a text document file)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/6lmuGmP.png">
<br />
<br />
<br />
<br />


 - Save the file with an extension of .jpg
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/teWiFwI.png">
<br />
<br />
<br />
<br />

 - We successfully recovered the jpg file!
<p align="center">
<br/>
<img width="680" alt="Portfolio" src="https://i.imgur.com/IAb1GZM.png">
<br />
<br />
<br />
<br />




\<end\>

[back to top](#toc)

<br />
<br />
<br />

