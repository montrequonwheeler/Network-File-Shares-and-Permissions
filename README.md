</p>

<h1>Network File Shares and Permissions</h1>
This walkthrough will build intuition for network file shares and permissions after the installation of our last Microsoft Active Directory Domain Services lab.  
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)
- Active Directory Domain Services

<h2>Operating Systems Used</h2>

- Windows Server 2022</b> (21H2)
- Windows 10</b> (21H2)

<h2>Create some sample file shares with various permissions</h2>

- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as a normal user (mydomain\<someuser>)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
- Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
- Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
- Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
- (Skip accounting for now)
<img width="1439" alt="FP 1" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/d6d91932-4307-4aef-9630-ea2349ac748e">
<img width="1439" alt="FP 2" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/517c6e28-89b5-4440-9dce-699083a67134">
<img width="1439" alt="FP 3" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/346a7dc0-b612-43ee-b484-76bb890d18f4">
<img width="1439" alt="FP 4" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/5d36ff4b-eeca-4592-96b7-190c6cb67a60">
<img width="1439" alt="FP 5" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/3d750e66-003f-4f40-aafb-17b30c5faa91">
<img width="1439" alt="FP 6" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/87d67229-c7d5-49e6-9126-5300c78be214">
<img width="1439" alt="FP 7" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/76d722c6-2af5-42a4-b30b-5c98e92e6e86">

<h2>Attempt to access file shares as a normal user</h2>

- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?

<img width="1439" alt="FP 8" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/34fc918d-50cf-4654-a02a-f5387c9927ad">
<img width="1439" alt="FP 9" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/3f765460-2689-48fe-aac2-7e0efcbb3082">
<img width="1440" alt="FP 11" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/cf6bbd9b-c312-4081-a152-1e0299d87db5">

- This message should appear if you try to create/write anything new, or access anything outside of client-1 permissions

<h2>Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</h2>

- Go back to DC-1, in Active Directory, create a organizational unit called “SECURITY_GROUPS”
- Go back to DC-1, in Active Directory, create a security group within it called “ACCOUNTANTS”
- On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
- On Client-1, as  <someuser>, try to access the accountants folder. It should fail. 
- Log out of Client-1 as  <someuser>
- On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
- Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?
<img width="1440" alt="FP 17" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/e0dd12aa-2779-4854-ab55-893e2419786b">
<img width="1440" alt="FP 16" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/3ee93cd1-ad1a-4fd7-8898-b15828943c3f">
<img width="1440" alt="FP 19" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/b76054d5-15f4-40e1-9d84-31432e3b89b4">
<img width="1440" alt="FP 20" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/c890490c-be0a-4e5b-b020-0aeb594fc017">
<img width="1440" alt="FP 21" src="https://github.com/montrequonwheeler/network-file-shares-and-permissions/assets/127397594/234e5870-bf8a-412c-a619-bfce686eea07">

- After you're finished, make sure to clean up by deleting all resource groups to avoid ongoing costs
