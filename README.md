# SFTP

     public static void main(String[] args) {
    	JSch jsch = new JSch();
	Session session = null;
	try {
	    session = jsch.getSession("kkgen_sftp", "203.146.107.234", 22);
	    session.setConfig("StrictHostKeyChecking", "no");
	    session.setPassword("GTGenkkftp1637");
	    session.connect();

	    Channel channel = session.openChannel("sftp");
	    channel.connect();
	    ChannelSftp sftpChannel = (ChannelSftp) channel;

	    File fileToUpload = new File("C:\\Users\\pratyay\\Documents\\Test.xlsx");
	    try {
				sftpChannel.put(new FileInputStream(fileToUpload), "/uploads/Test.xlsx");
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			}  
	    sftpChannel.exit();
	    session.disconnect();
	} catch (JSchException e) {
	    e.printStackTrace();  
	} catch (SftpException e) {
	    e.printStackTrace();
	}
    }
