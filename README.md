# SFTP

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
