# Java-Code-Snippets
Java Methods i'll be saving here, for personal future use.






Extracting files from a Zip, and putting one of them in memory -------------------------------->>>>>>>>>>>>>>>>>>>>>>>>>>>

    ----------------------------------------

            PEDING REFACTOR

    ----------------------------------------


<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< --------------------------------------------------------------------------------

public static void unzip(String zipFilePath /*, String destDir*/) throws Exception {
        int BUFFER = 2048;

        try {

            /*
            File dir = new File(destDir);
            if(!dir.exists()) {
                throw new Exception("No existe el directorio en el cual se extraera el archivo");
            }
            */


            BufferedOutputStream dest = null;
            BufferedInputStream is = null;

            ZipEntry entry;
            ZipFile zipfile = new ZipFile(zipFilePath);

            Enumeration e = zipfile.entries();
            while(e.hasMoreElements()) {
                entry = (ZipEntry) e.nextElement();
                System.out.println("Extrayendo : " +entry);

                is = new BufferedInputStream (zipfile.getInputStream(entry));
                int count;
                byte data[] = new byte[BUFFER];
//                FileOutputStream fos = new FileOutputStream(destDir + File.separator + entry.getName ());        dest = new BufferedOutputStream(fos, BUFFER);

                OutputStream out = new ByteArrayOutputStream();
                while ((count = is.read(data, 0, BUFFER)) != -1) {
//                    dest.write(data, 0, count);
                        out.write(data,0,count);
//                    System.out.println(is.read(data, 0, BUFFER));
                }

                System.out.println("A" + out);

//                dest.flush();
//                dest.close();
                is.close();
            }
        }
        catch(Exception e) {
            e.printStackTrace();
            throw new Exception();
        }
