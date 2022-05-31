# ASP.NET-IIS
## Configuring ASP.NET Website on IIS 

### Part 1: Create and build a website

Create ASP.NET Core Web App project on Visual Studio 2019

Install Newtonsoft.Json via NuGet Package Manager

Now if you go to csproj file you will see the following was added:
```
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
  </ItemGroup>
```

Right click on the solution and then click on "Restore Nuget Packages".
Go to build->Rebuild

Explanation of that step:
To promote a cleaner development environment and to reduce repository size, NuGet Package Restore installs all of a project's dependencies listed in either the project file or packages.config

Publish the application to a folder.

Now if you'll go to your project repo in the workspace folder than go to bin\Release\net5.0\publish
you will see an EXE file that you can run and then check your application is running locally via http://localhost:5001 as in the following screen shot:

![image](https://user-images.githubusercontent.com/88583978/171161946-62c5a82c-04e7-40dd-9eeb-923b26643e05.png)


### Part 2: Create website on Microsoft machine

1. On your local machine go to Remote Desktop Connection 
2. Press show options and insert the IP of the windows server and username and then press connect and you'll be asked for the password also
3. After successfuly connected to server go to Server Manager->Dashboard->add roles and features.
4. Add IIS to your windows server by installing all the relavant roles and features which is .NET framwork, ASP.NET, Web Server(IIS).
5. Go to IIS Manager->Application Pools and create a new IIS application pool
6. Navigate to the default website folder which should be within the path ```C:/inetpub/wwwroot``` and create a new folder with your site name
7. Go to sites->Add Website, select the application pool you've just created, insert your site name and port 5100 and for physical path insert the path of the folder you've just created in the previous step.
8. Copy all the files from the published folder created in part 1 to the folder you created in the previous steps (I did it by uploading the project to git and then downloaded on the server machine)
9. Now if you go to your website through ```http://localhost:5100/``` you will see an error 500.19

In order to fix it I used the following solution (installing Hosting Bundle Installer):

https://stackoverflow.com/questions/40805402/http-error-500-19-when-publish-net-core-project-into-iis-with-0x80070005

Now everything is ready and if you'll refresh the website you will see it's working as desired:

![image](https://user-images.githubusercontent.com/88583978/171167289-6a2893fe-1455-412d-8128-0c9e3cf719b3.png)

![image](https://user-images.githubusercontent.com/88583978/171167324-99a0f508-6085-4a2a-8be6-dcb86e888fef.png)

