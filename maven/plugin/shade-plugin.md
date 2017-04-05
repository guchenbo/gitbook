# 导出可执行jar，然后生成exe安装包

1. 导出jar包
	
	> maven项目使用shade plugin，将所需要的所有jar都打包到一个jar中

	> 示例：`<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-shade-plugin</artifactId>
				<version>1.7</version>

				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>shade</goal>
						</goals>
						<configuration>
							<finalName>handle-app-${project.version}</finalName>
							<shadedArtifactAttached>true</shadedArtifactAttached>
							<shadedClassifierName>jar-with-dependencies</shadedClassifierName>
							<transformers>
								<transformer
									implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
									<mainClass>cre.gutwo.swing.HandleFrame</mainClass>
								</transformer>
								<transformer
									implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
									<resource>META-INF/spring.handlers</resource>
								</transformer>
								<transformer
									implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
									<resource>META-INF/spring.schemas</resource>
								</transformer>
								<transformer
									implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
									<resource>META-INF/spring.tooling</resource>
								</transformer>
							</transformers>
						</configuration>
					</execution>
				</executions>
			</plugin>`

	> 使用方法：mvn clean install，会在target下找到handle-app-*.jar文件

2. 使用exe4j生成exe程序

	> 使用exe4j程序一步步生成exe，注意将%JAVA_HOME%jre目录作为jre搜索目录，可拷贝到程序根目录

3. 使用Inno Setup生成exe安装程序

	> 使用Inno Setup程序一步步生成exe安装包，将需要的目录打包到安装包中

