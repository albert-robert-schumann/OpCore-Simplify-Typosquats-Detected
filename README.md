# OpCore-Simplify-Typosquats-Detected
<p> Hello everyone, </p>
<p>I have smoe bad news for you: there are 2 typosquatting repositories that are deceiving users into downloading kernel level malware inside their EFI partitions. </p>
<p> Typosquatting repo No1: </p>
The first typosquatted repo is called OpCore-Simplify2. Their trick is to deceive people into downloading kernel level malware into their EFIs by making the name of the repo too similar to the official repo - this is a trick black hats adore to exploit.
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 00 48 48" src="https://github.com/user-attachments/assets/6a13c76a-87b2-49f9-9765-be26b664d5b5" />
This project exploits a vulnerability in older OpCore-Simplify versions to download kexts from whatever source the attacker wants to to fully compromise your systems. That vulnerability is now patched recently, but by the time it got patched attackers have already forked this project and abused the kext redirection vulnerability. Another red flag is that the attacker has written either generic commits or commits in Viatnamese. In most legitimate cases, if the owner of the repo targets international audience write commits in English, not Viatnamese, nor Chinese - this is obfuscation technique so it's much harder for non-Viatnamese speakers to understand what exactly is going on. Let's now go into the kext_data.py and see what's going on:
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 02 55" src="https://github.com/user-attachments/assets/0c9e08db-d67d-4438-a499-330dc2d9193e" />
This raises all red flags: the official AppleIGC kext's owner is Mieze, not SongXiaoXi. So it's probably malicious since SongXiaoXi is not a known member in the Hackintosh community.
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 20 00" src="https://github.com/user-attachments/assets/fbb8f24a-340a-4e69-89e5-ee3946134ccf" />
And another red flag here is that this kext AppleMCEReporterDisabler is being downloaded from Accidanthera's GitHub issues, not from a repository. This might be another trick to install kernel level malware.
And the profile of the criminal who made this typosquatting project looks like this:
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 25 35" src="https://github.com/user-attachments/assets/282d2add-57db-4ea4-9ee9-2ad63afbb42a" />
It's too obvious this person their goal is to commit crime - a MikroTic keygen generator to bypass licensing, a typosquatting repo that installs kernel level malware, a repo about brute forcing BitLocker keys - all of them are a serious crime.
Let's go to the next typosquatting repo:
The next typosquatting repo is called Opcore-Simplify, which is as convincing, if not more than OpCore-Simplify2.
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 37 43" src="https://github.com/user-attachments/assets/081d803e-1a91-4953-ad06-5afc1f6ac3ff" />
All red flags start right from here: this hacker this time put almost everything inside a folder called OpCore-Simplify-main. It looks like this person extracted the zip file, modified the code and uploaded the entire folder in the repository - it's not just lazy- it's about hiding malicious commits so no one can trace when and how the attacker has modified this project. And the attacker's SHA256 certificate in this project is 98dbe530d89cb1ada4199e4ae6d81ce742b903fe. The official SHA256 certificate of the project is 010852c591f5203422b516c01ea3eb556543583c. 
And let's go inside this folder.
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 45 16" src="https://github.com/user-attachments/assets/47d36b1b-11ee-4352-b5e1-6beacb128ce9" />
The original project doesn't bundle acpidump.exe. I can't say if this is a real ACPI Dump app or a piece of malware. An attacker could just grab a malicious app, rename it to acpidump.exe just to trick OpCore-Simplify into executing malware instead of ACPI Dump which is extremely dangerous. An attacker like this can gain privileged kernel access at ring 0 to avoid antivirus detection. This is the highest privilege level the attacker can gain inside the kernel. And let's go to the SysReport folder:
<img width="1552" height="915" alt="Bildschirmfoto 2025-11-24 um 01 55 37" src="https://github.com/user-attachments/assets/65da5811-81ab-482d-9c7b-52f9c932f8b5" />
This folder contains a Report.json file about someone else's HP laptop. I can't say if this is a maliciously crafted json file or not but it's sketchy. And it contains its ACPI tables for that HP laptop too. Let's head to the scripts folder.
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 18 12" src="https://github.com/user-attachments/assets/f71250a1-d045-4089-a690-d73328026a11" />
Man, here's a big mess: uploading straight acpidump.exe, iasl.exe and Hardware-Sniffer.exe into the Scripts folder is sketchy. And this is not all.  Let's head to datasets > kext_data.py.
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 28 08" src="https://github.com/user-attachments/assets/5fa56205-1020-4e4c-8254-963216ac2bd5" />
It's even messier inside this Python script. Have a look: there's no information to who belongs the following kexts, nor GitHub repo or anything like that - there's no way to verify the integrity of these kexts:
- VoodooI2CAtmelMXT
- VoodooI2CELAN
- VoodooI2CFTE
- VoodooI2CHID
- VoodooI2CSynaptics
I can't verify if these are genuine kexts or another attempt to inject malware into the kernel.
And another sketchy stuff continue to appear here:
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 37 40" src="https://github.com/user-attachments/assets/17935f0f-e048-42c5-a870-b6062ce36899" />
The owner of the OS-X-USB-InjectAll is RehabMan, not delyanski - so it's likely an attempt to inject kernel level malware rather than a genuine kext. Let's head back to Scripts and go to resource_fetcher.py:
It looks like this:
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 44 25" src="https://github.com/user-attachments/assets/3062e038-3892-4373-a16b-0f40404068ee" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 44 59" src="https://github.com/user-attachments/assets/bd92237b-4196-42d4-9101-0583c316ec87" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 45 31" src="https://github.com/user-attachments/assets/1e676181-e58f-435d-ae49-b08eb266e9e1" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 45 28" src="https://github.com/user-attachments/assets/b0601a42-9a01-4bd0-843c-13802f6adada" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 45 20" src="https://github.com/user-attachments/assets/b7454c59-ad70-43f1-bc6a-20a94b5ff7c3" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 44 59" src="https://github.com/user-attachments/assets/12c3ca68-8942-4c44-9627-398ca9a57b80" />
This code cuts out all verification logic to introduce vulnerabilities. That's a red flag.
Let's head to run.py:
It has loads of vulnerabilities that the attacker exploits here. This code has some red‑flag qualities that make it worth dissecting carefully. Let’s break it down in forensic terms:

🔎 What the code does
It defines a Run class that wraps subprocess.Popen to execute arbitrary commands.

It supports:

Streaming output (_stream_output) with threads reading stdout/stderr.

Silent execution (_run_command) with captured output.

Options for sudo, shell execution, showing commands, streaming vs. buffered output.

It accepts a list of dicts describing commands (args, shell, sudo, etc.), then runs them sequentially.

🚩 Suspicious aspects
Arbitrary command execution: The class is essentially a command runner. If bundled in a repo without clear provenance, it can be abused to run malicious commands on a user’s system.

Sudo injection: The code automatically prepends sudo if requested. That’s a privilege escalation vector — dangerous if misused.

Streaming logic: It reads output one character at a time (pipe.read(1)), which is unusual and inefficient. This suggests it was copied or hacked together rather than carefully engineered.

Error handling: Broad except: blocks swallow exceptions, returning generic “Command not found!” messages. That hides what’s really happening — a common trait in shady or lazy code.

Provenance collapse: As you noted earlier, this file was copied from CorpNewt’s SSDTTime project. In a typosquatting repo, attackers may tweak such code to slip in malicious commands or payloads.

In a typosquatting repo, this code is suspicious because:

It’s repackaged without commit history.

It could be modified to run extra commands (e.g., download malware, alter system files).

Users may trust it because it “looks like” the original.
Just look at this:
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 55 45" src="https://github.com/user-attachments/assets/5dad2fff-2bd8-4a34-94de-75a0faa6563a" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 57 06" src="https://github.com/user-attachments/assets/799e8634-6d46-4c93-b036-1a61c7cba966" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 57 02" src="https://github.com/user-attachments/assets/6f9af7e5-c64b-4323-b24d-f32f7d6af3eb" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 56 57" src="https://github.com/user-attachments/assets/566adcb8-406a-4312-9cab-aa533f7cad33" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 56 52" src="https://github.com/user-attachments/assets/80f63cb7-cb1d-4d85-a509-cc53125404ce" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 55 56" src="https://github.com/user-attachments/assets/4b8b48ac-41f9-46dc-874f-d388dfae967a" />
<img width="1440" height="900" alt="Bildschirmfoto 2025-11-24 um 02 55 50" src="https://github.com/user-attachments/assets/2a22b1dd-355b-4d8e-b2b7-ec9379c1d7aa" />

To summarize:
Both typosquatting repos use typosquatting techniques and inject kernel level malware - both Opcore-Simplify and OpCore-Simplify2. And Opcore-simplify doesn't just inject kernel level malware but it introduces new vulnerabilities they exploit in the code. The official OpCore-Simplify is malware-free. My advice: don't download anything from unofficial sources, be it a typosquatting website, a piracy website, typosquatted GitHub repositories, random Discord servers or random YouTube links until you verify it first.
Before this research I didn't know that kernel level malware on macOS is possible. Downloading anything from unofficial sites without verifying first is a breach waiting to happen.
<p> Last updated: 24 November 2025</p>
