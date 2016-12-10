---
layout: post
title:  "使用Maven构建Dubbo服务的可执行jar包 "
date:   2016-12-10 16:05:00
categories: Dubbo
---

# 使用Maven构建Dubbo服务的可执行jar包

Dubbo服务的运行方式：
1.使用servlet容器运行（Tomcat，Jetty等） --- 不可取

	缺点： 增加复杂性（端口、管理）
			浪费资源（内存）

2.自建Main方法类来运行（Spring容器） --- 不建议（本地调试可用）

	缺点： Dubbo本身提供的高级特性没有用上
			自己编写启动类可能会有缺陷
		
3.使用Dubbo框架提供的main方法类来运行（Spring容器）--- 建议使用

	优点：框架本身提供（com.alibaba.dubbo.container.Main)
			可实现优雅关机（shutdownHook）
		
注意点:
spring-context.xml,```<import resource="classpath:spring/spring-xxx.xml"/>```




	<build>
		<finalName>edu-service-user</finalName>
		<resources>
			<resource>
				<targetPath>${project.build.directory}/classes</targetPath>
				<directory>src/main/resources</directory>
				<filtering>true</filtering>
				<includes>
					<include>**/*.xml</include>
					<include>**/*.properties</include>
				</includes>
			</resource>
			<!-- 结合com.alibaba.dubbo.container.Main -->
			<resource>
				<targetPath>${project.build.directory}/classes/META-INF/spring</targetPath>
				<directory>src/main/resources/spring</directory>
				<filtering>true</filtering>
				<includes>
					<include>spring-context.xml</include>
				</includes>
			</resource>
		</resources>
		
		<pluginManagement>
			<plugins>
				<!-- 解决Maven插件在Eclipse内执行了一系列的生命周期引起冲突 -->
				<plugin>
					<groupId>org.eclipse.m2e</groupId>
					<artifactId>lifecycle-mapping</artifactId>
					<version>1.0.0</version>
					<configuration>
						<lifecycleMappingMetadata>
							<pluginExecutions>
								<pluginExecution>
									<pluginExecutionFilter>
										<groupId>org.apache.maven.plugins</groupId>
										<artifactId>maven-dependency-plugin</artifactId>
										<versionRange>[2.0,)</versionRange>
										<goals>
											<goal>copy-dependencies</goal>
										</goals>
									</pluginExecutionFilter>
									<action>
										<ignore />
									</action>
								</pluginExecution>
							</pluginExecutions>
						</lifecycleMappingMetadata>
					</configuration>
				</plugin>
			</plugins>
		</pluginManagement>
		<plugins>
			<!-- 打包jar文件时，配置manifest文件，加入lib包的jar依赖 -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<configuration>
					<classesDirectory>target/classes/</classesDirectory>
					<archive>
						<manifest>
							<mainClass>com.alibaba.dubbo.container.Main</mainClass>
							<!-- 打包时 MANIFEST.MF文件不记录的时间戳版本 -->
							<useUniqueVersions>false</useUniqueVersions>
							<addClasspath>true</addClasspath>
							<classpathPrefix>lib/</classpathPrefix>
						</manifest>
						<manifestEntries>
							<Class-Path>.</Class-Path>
						</manifestEntries>
					</archive>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-dependency-plugin</artifactId>
				<executions>
					<execution>
						<id>copy-dependencies</id>
						<phase>package</phase>
						<goals>
							<goal>copy-dependencies</goal>
						</goals>
						<configuration>
							<type>jar</type>
							<includeTypes>jar</includeTypes>
							<useUniqueVersions>false</useUniqueVersions>
							<outputDirectory>
								${project.build.directory}/lib
							</outputDirectory>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>	


