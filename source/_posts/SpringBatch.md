---
title: Spring Batch
date: 2022-05-17 18:34:12
tags:
- Java
categories:
- 学习
- Java
---



**There are two types of steps provided by Spring Batch.**

- Tasklet Step
- Chunk-Oriented Step



There are different options we can launch our job. We can use REST API to trigger job and we can use Spring Scheduler to schedule Spring Batch Job. Also we can stop Job using REST API.

<!-- more -->

**There are different Item Readers provided by Spring Batch.**

- CSV Item Reader
- JSON Item Reader
- XML Item Reader
- JDBC Item Reader
- REST API Item Reader



**There are different Item Writers provided by Spring Batch.**

- CSV Item Writer
- JSON Item Writer
- XML Item Writer
- JDBC Item Writer
- REST API Item Writer



Spring Batch Provides Item Processor to process data. Item Processor is in between Item Reader & Item Writer.

![image-20220517230657681](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202205172306783.png)



## 1.Demo Project

```java
@Configuration
public class SampleJob {

	@Autowired
	private JobBuilderFactory jobBuilderFactory;

	@Autowired
	private StepBuilderFactory stepBuilderFactory;
	
	@Autowired
	private SecondTasklet secondTasklet;

	@Bean
	public Job firstJob() {
		return jobBuilderFactory.get("First Job")
				.start(firstStep())
				.next(secondStep())
				.build();
	}

	private Step firstStep() {
		return stepBuilderFactory.get("First Step")
				.tasklet(firstTask())
				.build();
	}

	private Tasklet firstTask() {
		return new Tasklet() {

			@Override
			public RepeatStatus execute(StepContribution contribution, ChunkContext chunkContext) throws Exception {
				System.out.println("This is first tasklet step");
				return RepeatStatus.FINISHED;
			}
		};
	}
	
	private Step secondStep() {
		return stepBuilderFactory.get("Second Step")
				.tasklet(secondTasklet)
				.build();
	}

}
```



```java
@Service
public class SecondTasklet implements Tasklet {

	@Override
	public RepeatStatus execute(StepContribution contribution, ChunkContext chunkContext) throws Exception {
		System.out.println("This is second tasklet step");
		return RepeatStatus.FINISHED;
	}

}
```



