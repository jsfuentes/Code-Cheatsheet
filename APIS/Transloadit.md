# Transloadit

- Useful for large files like videos
- Download, Upload, transcode, and push to an S3/server

## Basics

You create a **template** that has a JSON describing the list of steps or **robots** and their settings

Use the opensource tool [**Uppy**](https://uppy.io/) to upload files, comes with nice upload UI for different sources even GDrive and camera out of the box

Use [Robodog](https://uppy.io/docs/robodog/), the uppy based library to talk to Transloadit API

```javascript
import Robodog from "@uppy/robodog";

const resultPromise = Robodog.upload(files, {
  params: {
    auth: { key: "3.dsafkjads.adsf.afds.adsf.." },
    steps: {
      ":original": {
        robot: "/upload/handle",
      },
      export: {
        use: ":original",
        robot: "/s3/store",
        credentials: "eta-aws",
        //\$ for translodits string stuff url_name is url encoded name with extension
        path: `${new Date().toISOString()}-\${file.url_name}`,
      },
    },
  },
});

resultPromise.then((bundle) => {
  bundle.transloadit // Array of Assembly statuses
  
})
```

#### Templates

Here is a basic template to output .webm

Can use assembly variables like `${fields.*}` if uppy was set to allow it

```json
{
  "steps": {
    ":original": {
      "robot": "/upload/handle"
    },
    "filter": {
      "use": ":original",
      "robot": "/file/filter",
      "accepts": [
        [
          "${file.mime}",
          "regex",
          "video"
        ]
      ],
      "error_on_decline": true
    },
    "video_webm": {
      "use": "filter",
      "robot": "/video/encode",
      "ffmpeg_stack": "v3.3.3",
      "preset": "webm"
    },
    "export": {
      "use": [
        "video_webm"
      ],
      "robot": "/s3/store",
      "credentials": "slingshow_aws",
    }
  }
}
```

Then credientials should be set in template credentials

