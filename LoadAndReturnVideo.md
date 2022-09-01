# Load And Return video from localstorage

public ResponseEntity<?> playTheVideo(){
	logger.info("I am here ======================================");
	try {
		File filePath = new File ("/home/raosaheb/Desktop/t1.mp4");
		ByteArrayOutputStream baos = new ByteArrayOutputStream();
		FileInputStream fis = new FileInputStream(new File("/home/raosaheb/Desktop/t1.mp4"));

		byte[] buf = new byte[1024];
		int n;
		while (-1 != (n = fis.read(buf)))
		    baos.write(buf, 0, n);

		byte[] videoBytes = baos.toByteArray();

	    return ResponseEntity.ok()
	            .contentType(MediaType.parseMediaType("video/mp4"))
	            .header(HttpHeaders.CONTENT_DISPOSITION, String.format("attachment; filename=video_%s.%s", 1, "mp4"))
	            .body(videoBytes);
	} catch (Exception e) {
		return new ResponseEntity<>(e.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
	}
}



#play video from browser
		@GetMapping(value = "/playVideo")
		public final ResponseEntity<?> playDemoVideo() {
			try {
				File initialFile = new File(config.getVkycDemoVideoFilePath());
				InputStream targetStream = new FileInputStream(initialFile);
				HttpHeaders headers = new HttpHeaders();
				headers.setContentType(MediaType.valueOf("video/mp4"));
				headers.set("Accept-Ranges", "bytes");
				headers.set("Expires", "0");
				headers.set("Cache-Control", "no-cache, no-store");
				headers.set("Connection", "keep-alive");
				headers.set("Content-Transfer-Encoding", "binary");

				return new ResponseEntity<>(new InputStreamResource(targetStream), headers,
						org.springframework.http.HttpStatus.OK);
			} catch (Exception e) {
				return new ResponseEntity<>("Failed To play The video",
						org.springframework.http.HttpStatus.INTERNAL_SERVER_ERROR);
			}

		}
		
	
#Play video in Jsp and control 

1. Go to Jsp Page 
public String goToJsp(){
	return playVideo.jsp
}

2. playVideo.jsp
	<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
video {
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
}
</style>
<title>demo</title>
</head>
<body style="background-color: black;">

<div class="media-box foto">
  <video style="align-content: center;" src="https://localhost:8090/vi/playVideo"
         width="25%" height="25%" controls>
    <p>Your browser does not support HTML5 video. Here is a <a href="https://localhost:8090/vi/playVideo">link to the video</a> instead.</p>
  </video>
</div>

</body>
</html>

3. Load Video in Jsp page 

@GetMapping(value = "/playVideo")
		public final ResponseEntity<?> playDemoVideo() {
			try {
				File initialFile = new File(config.getVkycDemoVideoFilePath());
				InputStream targetStream = new FileInputStream(initialFile);
				HttpHeaders headers = new HttpHeaders();
				headers.setContentType(MediaType.valueOf("video/mp4"));
				headers.set("Accept-Ranges", "bytes");
				headers.set("Expires", "0");
				headers.set("Cache-Control", "no-cache, no-store");
				headers.set("Connection", "keep-alive");
				headers.set("Content-Transfer-Encoding", "binary");

				return new ResponseEntity<>(new InputStreamResource(targetStream), headers,
						org.springframework.http.HttpStatus.OK);
			} catch (Exception e) {
				return new ResponseEntity<>("Failed To play The video",
						org.springframework.http.HttpStatus.INTERNAL_SERVER_ERROR);
			}

		}




