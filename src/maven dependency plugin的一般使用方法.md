# maven dependency plugin的一般使用方法 #

pom写法：

			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-dependency-plugin</artifactId>
				<version>2.10</version>
				<executions>
					<execution>
						<id>analyze</id>
						<phase>package</phase>
						<goals>
							<goal>analyze</goal>
						</goals>
						<inherited>false</inherited>
					</execution>
					<execution>
						<id>copy</id>
						<phase>package</phase>
						<goals>
							<goal>copy-dependencies</goal>
						</goals>
						<inherited>false</inherited>
					</execution>
				</executions>
				<configuration>
					<includeScope>compile</includeScope>
				</configuration>
			</plugin>


命令用法：
	 
	mvn dependency:analyze

    mvn dependency:copy-dependencies
