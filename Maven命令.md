##Maven 学习笔记 

| 命令 |  功能 | 备注 |
| --- | --- | --- |
| mvn -v  | 查看maven版本 |
| mvn help:system   |  查看maven配置的系统信息 |
| mvn archetype:generate | 构建项目目录结构 | 在要建立项目的目录下运行 |
| mvn clean build | 项目构建 |  从远程仓库下载jar包 |
| mvn clean compile | 项目编译 |
| mvn clean package | 项目打包 |   |
| mvn clean install | 项目安装 |  将打包后的项目安装到本地仓库 |
| mvn clean install -U |  | 强制检查更新，使用最新版本的依赖包|
| mvn clean test   |  项目测试 | 
| mvn dependency:list | 查看项目依赖 |  列表显示 |
| mvn dependency:tree | 查看项目依赖 |  树状显示 |
| mvn dependency:analyze | 项目依赖分析  |
| mvn clean deploy | 项目部署到远程仓库 | 
| mvn clean package -Dmaven.test.skip=true | 跳过测试 |  
| mvn clean install `-pl`  artifactId1,artifactId2 | 指定构建某个模块|  多个模块用,分隔，不会构建依赖模块 |
| mvn clean install `-pl ` Id1,Id2 `-am` | |构建指定模块，同时构建所列模块的依赖模块 |
| mvn clean install `-pl`  Id1,Id2 `-amd` | |构建指定模块，同时构建依赖于所列模块的模块 |
| mvn clean install `-rf` Id1 | |构建指定模块，同时指定从哪个模块开始构建 |
| mvn clean install `-pl` Id1,Id2,Id3 `-amd` `-rf` Id2||裁剪发应堆，指定从Id2开始构建|
| mvn install:install-file  </br>-DgroupId=com.google.code </br>-DartifactId=kaptcha </br>-Dversion=2.3.2 </br>-Dfile=kaptcha-2.3.2.jar </br>-Dpackaging=jar </br>-DgeneratePom=true | | 安装第三方jar到本地库中|
| mvn package -DskipTests| 跳过测试的运行||
| mvn package -Dmavne.test.skip=ture| 跳过测试的运行，并跳过测试代码的编译|  
| mvn test -Dtest = RandomTest | 只运行指定类名的测试 |
| mvn test -Dtest = Random\*Test | 只运行指定类名的测试 | 可以加通配符，指定测试多个类|
| mvn test -Dtest = Random1Test ,Random2Test |   | 可以指定多个类，用,分隔 |
| mvn test -Dtest = Random\*Test ,Random2Test |   | 多个类测试，讲法可以混合使用  |
| mvn test -Dtest -DfailIfNoTests=false| 没有任何测试都不要报错 | 相当于跳过测试 |
| mvn cobertura:cobertura | 生成测试覆盖率报告 |  应该是用的javadoc机制，在项目的target目录，生成site目录，里面index.html为报告入口|