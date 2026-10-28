# GameZone-Rental-PlayStation
GameZone Rental PlayStation adalah aplikasi berbasis console yang dibuat menggunakan bahasa pemrograman Java. Aplikasi ini membantu petugas menghitung biaya penyewaan PlayStation 4 dan PlayStation 5. cara menjalankan program : Unduh atau clone repositori ini. Buka project melalui Apache NetBeans IDE. Buka class GameZone.java. Jalankan program. ## Screenshot Output
![Hasil program GameZone](<img width="557" height="634" alt="output gamezone" src="https://github.com/user-attachments/assets/3605b7a0-1297-45fd-821e-f0e98c336563" />)

[GameZone.java](https://github.com/user-attachments/files/34089862/GameZone.java)

import java.util.Scanner;

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */

/**
 *
 * @author FILDZAH
 */
public class GameZone {
    
    static Scanner input = new Scanner(System.in);
    
    // Method untuk menjalankan program
    public static void main(String[] args) {
        String transaksiBaru;
        
        do {
            prosesTransaksi();
            
            System.out.print("\nTransaksi Baru (Y/T): ");
            transaksiBaru = input.nextLine().trim();
            
            while (!transaksiBaru.equalsIgnoreCase("Y") && !transaksiBaru.equalsIgnoreCase("T")) {
              System.out.print("Input tidak valid. Masukkan Y atau T: ");
              transaksiBaru = input.nextLine().trim();
            }
            
        } while (transaksiBaru.equalsIgnoreCase("Y"));
        
         System.out.println("\nTerima kasih telah menggunakan " + "GameZone Rental PS!");
        input.close();
    }
    
     // Method untuk memproses transaksi penyewaan
    public static void prosesTransaksi() {

        String namaPelanggan;
        String namaKonsol = "";
        String pilihanMinuman;
        int pilihanKonsol;
        int hargaPerJam = 0;
        int durasi;
        int biayaSewa;
        int diskon = 0;
        int biayaMinuman = 0;
        int totalBayar;
        
         System.out.println("\n====================================");
        System.out.println("          GAMEZONE RENTAL PS");
        System.out.println("====================================");
        
         // Input nama pelanggan
        do {
            System.out.print("Nama Pelanggan : ");
            namaPelanggan = input.nextLine().trim();
            
          if (namaPelanggan.isEmpty()) {
                System.out.println("Nama tidak boleh kosong.");
            }
        } while (namaPelanggan.isEmpty());
        
        // Pilihan konsol
        System.out.println("\nPilihan Konsol:");
        System.out.println("1. PlayStation 4 - Rp8000/jam");
        System.out.println("2. PlayStation 5 - Rp12000/jam");

        System.out.print("Pilihan         : ");
        pilihanKonsol = bacaBilanganBulat();
        
          // Menentukan jenis konsol dan harga
        while (pilihanKonsol != 1 && pilihanKonsol != 2) {
            System.out.print("Pilihan tidak valid. Masukkan 1 atau 2: ");
            pilihanKonsol = bacaBilanganBulat();
        }
        
         switch (pilihanKonsol) {
            case 1:
                namaKonsol = "PlayStation 4";
                hargaPerJam = 8000;
                break;
                
              case 2:
                namaKonsol = "PlayStation 5";
                hargaPerJam = 12000;
                break;

            default:
                System.out.println("Pilihan tidak tersedia.");
        }   
         
         // Input durasi bermain
        System.out.print("Lama Bermain (jam): ");
        durasi = bacaBilanganBulat();

       while (durasi <= 0) {
            System.out.print("Durasi harus lebih dari 0 jam: ");
            durasi = bacaBilanganBulat();
        }

        // Menghitung biaya sewa
        biayaSewa = hargaPerJam * durasi;
        
        // Menghitung diskon 10% untuk minimal 3 jam
        if (durasi >= 3) {
            diskon = biayaSewa * 10 / 100;
        } else {
            diskon = 0;
        }

        // Pilihan minuman
        System.out.print("Tambah Minuman (Y/T): ");
        pilihanMinuman = input.nextLine().trim();

        while (!pilihanMinuman.equalsIgnoreCase("Y")
                && !pilihanMinuman.equalsIgnoreCase("T")) {
            System.out.print("Input tidak valid. Masukkan Y atau T: ");
            pilihanMinuman = input.nextLine().trim();
        }
        
        if (pilihanMinuman.equalsIgnoreCase("Y")) {
            biayaMinuman = 5000;
        } else {
            biayaMinuman = 0;
        }
        
          // Menghitung total pembayaran
        totalBayar = biayaSewa - diskon + biayaMinuman;

        // Menampilkan struk transaksi
        cetakStruk(
                namaPelanggan,
                namaKonsol,
                durasi,
                biayaSewa,
                diskon,
                biayaMinuman,
                totalBayar
        );
    }
    
     // Method untuk membaca bilangan bulat dengan aman
    public static int bacaBilanganBulat() {
        while (true) {
            String teks = input.nextLine().trim();

            try {
                return Integer.parseInt(teks);
            } catch (NumberFormatException e) {
                System.out.print("Input harus berupa bilangan bulat. Masukkan lagi: ");
            }
        }
    }
    
     // Method untuk mencetak struk pembayaran
    public static void cetakStruk(
            String namaPelanggan,
            String namaKonsol,
            int durasi,
            int biayaSewa,
            int diskon,
            int biayaMinuman,
            int totalBayar) {

        System.out.println("\n------------------------------------");
        System.out.println("            STRUK GAMEZONE");
        System.out.println("------------------------------------");
        
          System.out.println("Pelanggan       : " + namaPelanggan);
        System.out.println("Konsol          : " + namaKonsol);
        System.out.println("Durasi          : " + durasi + " jam");
        System.out.println("Biaya Sewa      : Rp" + biayaSewa);
        System.out.println("Diskon (10%)    : Rp" + diskon);
        System.out.println("Minuman         : Rp" + biayaMinuman);

        System.out.println("------------------------------------");
        System.out.println("TOTAL BAYAR     : Rp" + totalBayar);
        System.out.println("====================================");
    }
}

