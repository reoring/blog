---
template: BlogPost
path: /golang/aws/credentials
date: 2020-12-19T11:54:30.069Z
title: Go言語でAWS SDKを使ったときにCredentials読み込まれないときの対処
metaDescription: ''
---
```go
	sess, err := session.NewSessionWithOptions(session.Options{
		// Specify profile to load for the session's config
		//Profile: "profile_name",
	
		// Provide SDK Config options, such as Region.
		Config: aws.Config{
			Region: aws.String("ap-northeast-1"),
		},
	
		// Force enable Shared Config support
		SharedConfigState: session.SharedConfigEnable,
	})
```

このようにNewSessionWithOptionsでSessionを生成するときに、SharedConfigEnableを指定するとよい。
