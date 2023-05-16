Please do below changes to make application runnable.

1. create  ExternalOutboundChannel.java

package com.lti;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/v1")
public class ExternalOutboundChannel {

	@PostMapping("/outbound")
	String outbound(@RequestBody String str) {
		System.out.print("External channel : message recevied !  " + str);
		return str;
	}
}

2. Add below http outbound channel

<integration:channel id="out" />
	<!--  Print json object in external service -->
	<int-http:outbound-channel-adapter
		id="externalService" url="http://localhost:8080/v1/outbound"
		channel="out" http-method="POST" charset="UTF-8"
		auto-startup="true" />