[![Build Status](https://travis-ci.org/sendgrid/sendgrid-go.svg?branch=v3beta)](https://travis-ci.org/sendgrid/sendgrid-go) [![GoDoc](https://godoc.org/github.com/sendgrid/rest?status.png)](http://godoc.org/github.com/sendgrid/sendgrid-go)

**This library allows you to quickly and easily use the SendGrid Web API via Go.**

*NOTE: The `/mail/send/beta` endpoint is currently in beta!

Since this is not a general release, we do not recommend POSTing production level traffic through this endpoint or integrating your production servers with this endpoint.

When this endpoint is ready for general release, your code will require an update in order to use the official URI.

By using this endpoint, you accept that you may encounter bugs and that the endpoint may be taken down for maintenance at any time. We cannot guarantee the continued availability of this beta endpoint. We hope that you like this new endpoint and we appreciate any [feedback](dx+mail-beta@sendgrid.com) that you can send our way.**

# Installation

`go get github.com/sendgrid/sendgrid-go`

```go
import "github.com/sendgrid/sendgrid-go"
```

## Dependencies

- [rest](https://github.com/sendgrid/rest)

## Environment Variables

First, get your free SendGrid account [here](https://sendgrid.com/free?source=sendgrid-go).

Next, update your environment with your [SENDGRID_API_KEY](https://app.sendgrid.com/settings/api_keys).

```bash
echo "export SENDGRID_API_KEY='YOUR_API_KEY'" > sendgrid.env
echo "sendgrid.env" >> .gitignore
source ./sendgrid.env
```

# Quick Start

## Hello Email
```go
import (
	"encoding/json"
	"fmt"
	"github.com/sendgrid/sendgrid-go"
	"github.com/sendgrid/sendgrid-go/helpers/mail"
	"os"
)
from := mail.NewEmail("DX", "dx@sendgrid.com")
subject := "Hello World from the SendGrid Go Library"
to := mail.NewEmail("Elmer Thomas", "elmer.thomas@sendgrid.com")
content := mail.NewContent("text/plain", "some text here")
m := mail.NewV3MailInit(from, subject, to, content)

b, err := json.Marshal(m)
if err != nil {
    fmt.Println(err)
}
request := sendgrid.GetRequest(os.Getenv("SENDGRID_API_KEY"), "/mail/send/beta", "https://api.sendgrid.com", "v3")
request.Method = "POST"
var requestBody = []byte(string(b))
request.RequestBody = requestBody
response, err := sendgrid.API(request)
if err != nil {
    fmt.Println(err)
} else {
    fmt.Println(response.StatusCode)
    fmt.Println(response.ResponseBody)
    fmt.Println(response.ResponseHeaders)
}
```

## General v3 Web API Usage

```go
import (
	"fmt"
	"github.com/sendgrid/sendgrid-go"
	"os"
)

func main() {
    request := sendgrid.GetRequest(os.Getenv("SENDGRID_API_KEY"), "/api_keys", "https://api.sendgrid.com", "v3")
    request.Method = "GET"

    response, err := sendgrid.API(request)
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println(response.StatusCode)
        fmt.Println(response.ResponseBody)
        fmt.Println(response.ResponseHeaders)
    }
}
```

# Announcements

**BREAKING CHANGE as of XXXX.XX.XX**

Version `3.0.0` is a breaking change for the entire library.

Version 3.0.0 brings you full support for all Web API v3 endpoints. We
have the following resources to get you started quickly:

-   [SendGrid
    Documentation](https://sendgrid.com/docs/API_Reference/Web_API_v3/index.html)
-   [Usage
    Documentation](https://github.com/sendgrid/sendgrid-go/tree/v3beta/USAGE.md)
-   [Example
    Code](https://github.com/sendgrid/sendgrid-go/tree/v3beta/examples)

Thank you for your continued support!

## Roadmap

[Milestones](https://github.com/sendgrid/sendgrid-go/milestones)

## How to Contribute

We encourage contribution to our libraries, please see our [CONTRIBUTING](https://github.com/sendgrid/sendgrid-go/tree/v3beta/CONTRIBUTING.md) guide for details.

* [Feature Request](https://github.com/sendgrid/sendgrid-go/tree/v3beta/CONTRIBUTING.md#feature_request)
* [Bug Reports](https://github.com/sendgrid/sendgrid-go/tree/v3beta/CONTRIBUTING.md#submit_a_bug_report)
* [Improvements to the Codebase](https://github.com/sendgrid/sendgrid-go/tree/v3beta/CONTRIBUTING.md#improvements_to_the_codebase)

## Usage

- [SendGrid Docs](https://sendgrid.com/docs/API_Reference/index.html)
- [v3 Web API](https://github.com/sendgrid/sendgrid-go/tree/v3beta/USAGE.md)
- [Example Code](https://github.com/sendgrid/sendgrid-go/tree/v3beta/examples)
- [v3 Web API Mail Send Helper](https://github.com/sendgrid/sendgrid-go/tree/v3beta/helpers/mail/README.md)

## Unsupported Libraries

- [Official and Unsupported SendGrid Libraries](https://sendgrid.com/docs/Integrate/libraries.html)

# About

![SendGrid Logo]
(https://assets3.sendgrid.com/mkt/assets/logos_brands/small/sglogo_2015_blue-9c87423c2ff2ff393ebce1ab3bd018a4.png)

sendgrid-go is guided and supported by the SendGrid [Developer Experience Team](mailto:dx@sendgrid.com).

sendgrid-go is maintained and funded by SendGrid, Inc. The names and logos for sendgrid-go are trademarks of SendGrid, Inc.
