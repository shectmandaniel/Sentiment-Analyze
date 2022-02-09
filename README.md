# sentiment

### stanford sentiment analysis
```
		<dependency>
			<groupId>edu.stanford.nlp</groupId>
			<artifactId>stanford-corenlp</artifactId>
			<version>3.8.0</version>
		</dependency>

		<dependency>
			<groupId>edu.stanford.nlp</groupId>
			<artifactId>stanford-corenlp</artifactId>
			<version>3.8.0</version>
			<classifier>models</classifier>
		</dependency>
```
apply patch stanford
commit - with nlp
### twitter
pom.xml
```
		<dependency>
			<groupId>org.twitter4j</groupId>
			<artifactId>twitter4j-core</artifactId>
			<version>4.0.7</version>
		</dependency>

		<dependency>
			<groupId>org.twitter4j</groupId>
			<artifactId>twitter4j-async</artifactId>
			<version>4.0.7</version>
		</dependency>

		<dependency>
			<groupId>org.twitter4j</groupId>
			<artifactId>twitter4j-stream</artifactId>
			<version>4.0.7</version>
		</dependency>
```

apply patch - twitter
<br>
controller/AppController.java
```java

    @RequestMapping(path = "/startTwitter", method = RequestMethod.GET)
    public  @ResponseBody Flux<String> start(String text)  {
        return twitterStream.filter(text)
                .window(Duration.ofSeconds(3))
                .flatMap(window->toArrayList(window))
                .map(messages->{
                    if (messages.size() == 0) return "size: 0 <br>";
                    return "size: " + messages.size() + "<br>";
                });
    }

    @RequestMapping(path = "/stopTwitter", method = RequestMethod.GET)
    public  @ResponseBody Mono<String> stop()  {
        twitterStream.shutdown();
        return Mono.just("shutdown");
    }

    public static <T> Mono<ArrayList<T>> toArrayList(Flux<T> source) {
        return  source.reduce(new ArrayList(), (a, b) -> { a.add(b);return a; });
    }
```
commit - with twitter
