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
