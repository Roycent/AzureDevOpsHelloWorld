# Azure DevOps

- 创建项目
![create](img/1-CreateProject.png)
- 项目主页
![homepage](img/2-WelcomePage.png)
- 创建新"Pipeline"
![newPipeline](img/3-NewPipeline.png)
- 选择Github代码仓库
![selectGithub](img/4-PipelineConnectGithub.png)
- 在代码仓库中加入Pipeline配置代码
![install](img/6-InstallPipeline.png)
- 选择Pipeline基础配置（之后还可以详细自定义配置文件）
![configure](img/7-ConfigurePipeline.png)
- 编辑Pipeline配置文件
![edit](img/8-EditPipelineConfig.png)
在默认的配置文件中，加入发布task一节；同时因为并没有编写测试，删除测试的那节

    ```yaml
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: 'artifact'
        publishLocation: 'Container'
    ```

- 执行`Save and run`，会在Github仓库中新增在上面编辑好的yaml配置文件，同时也可以自定义自己的提交信息
![saveAndRun](img/9-SaveAndRunBuild.png)
- Build成功
![buildSuccess](img/10-BuildSuccess.png)
- 新建Release Pipeline
![releasePip](img/11-ReleasePipeline.png)
- 选择模板，以使用IIS发布为例
![selectRelT](img/12-ReleaseTemplate.png)
- 新建阶段
![selectStage](img/13-SelectStage.png)
- 新建部署组
![deploymentGroup](img/14-DeploymentGroup.png)
- 在要部署的服务器上复制右侧的脚本并运行即可
![agent](img/15-AddAgent.png)
- 新建Release Pipeline，以在IIS上、web app deploy方式部署的网站为例
![releasePipeline](img/16-NewRelease.png)
- 点击`Pipeline`，添加Artifact
![add](img/17-AddArt.png)
- 然后点击右上角的`Save`和`Create Release`
![goingToDeploy](img/18-BeforeDeploy.png)
- 点击`Deploy`
![success](img/19-DeploySuccess.png)
- 部署成功

## 常见错误

### 在release时报错

错误信息为`no package found with specified pattern`

默认的build配置中并没有生成artifact，所以要手动添加生成artifact

### 部署成功后网站仍无法访问

确认网站的类型，有些是无托管代码的，应用程序池要设置为无托管代码
