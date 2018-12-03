# SFTP

library https://mvnrepository.com/artifact/com.jcraft/jsch

     public static void main(String[] args) {
		JSch jsch = new JSch();
        	Session session = null;
        
		try {

		    session = jsch.getSession("username", "111.111.111.111", 22);
		    session.setConfig("StrictHostKeyChecking", "no");
		    session.setPassword("password");
		    session.connect();

		    Channel channel = session.openChannel("sftp");
		    channel.connect();
		    ChannelSftp sftpChannel = (ChannelSftp) channel;

		    File fileToUpload = new File("C:\\Users\\pratyay\\Documents\\Test.xlsx");
		    sftpChannel.put(new FileInputStream(fileToUpload), "/uploads/Test.xlsx", ChannelSftp.OVERWRITE);

		    sftpChannel.exit();
		    session.disconnect();

		} catch (JSchException | SftpException | FileNotFoundException e) {
		    e.printStackTrace();  
		}  
    }
    
# FTP
library https://mvnrepository.com/artifact/commons-net/commons-net/3.6
	
	public static void main(String[] args) {
		
		FTPClient client = new FTPClient();
		FileInputStream fis = null;
		
		try {
			
			client.connect("ftp.xxxxxxxxx.com",21);
			client.login("xxxx", "xxxxxx");
			client.enterLocalPassiveMode();
			//client.setFileType(FTP.BINARY_FILE_TYPE);
			
			File filename = new File("C:\\Users\\pratyay\\Documents\\Test.xlsx");
			FileInputStream fileInputStream = new FileInputStream(filename);
			
			boolean isComplete = client.storeFile("/domains/barokahthailand.com/photo/Test.xlsx", fileInputStream);
			System.out.println(isComplete);
			
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			
			if (client != null && client.isConnected()) {
				client.logout();
				client.disconnect();
			}
		}
	}
