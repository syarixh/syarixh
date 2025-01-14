import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;

public class KasirRumahMakan {
    static HashMap<String, Double> menu = new HashMap<>();
    static ArrayList<Pesanan> pesananList = new ArrayList<>();

    static class Pesanan {
        String namaMakanan;
        int jumlah;
        double harga;

        Pesanan(String namaMakanan, int jumlah, double harga) {
            this.namaMakanan = namaMakanan;
            this.jumlah = jumlah;
            this.harga = harga;
        }

        double totalHarga() {
            return jumlah * harga;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        menu.put("Nasi Goreng", 20000.0);
        menu.put("Mie Goreng", 15000.0);
        menu.put("Ayam Penyet", 25000.0);
        menu.put("Sate Ayam", 30000.0);
        menu.put("Es Teh", 5000.0);
        menu.put("Es Jeruk", 7000.0);

        System.out.println("Selamat datang di Rumah Makan!");
        boolean lanjut = true;

        while (lanjut) {
            System.out.println("\nMenu:");
            for (String makanan : menu.keySet()) {
                System.out.println(makanan + " - Rp " + menu.get(makanan));
            }

            System.out.print("Masukkan nama makanan (atau ketik 'selesai' untuk selesai): ");
            String namaMakanan = scanner.nextLine();

            if (namaMakanan.equalsIgnoreCase("selesai")) {
                lanjut = false;
                continue;
            }

            if (!menu.containsKey(namaMakanan)) {
                System.out.println("Makanan tidak tersedia. Silakan coba lagi.");
                continue;
            }

            System.out.print("Masukkan jumlah: ");
            int jumlah = scanner.nextInt();
            scanner.nextLine(); // membersihkan newline

            double harga = menu.get(namaMakanan);
            pesananList.add(new Pesanan(namaMakanan, jumlah, harga));
            System.out.println("Pesanan ditambahkan: " + namaMakanan + " x " + jumlah);
        }

        double totalBayar = 0;
        System.out.println("\nStruk Pembayaran:");
        for (Pesanan pesanan : pesananList) {
            double totalPesanan = pesanan.totalHarga();
            System.out.println(pesanan.namaMakanan + " x " + pesanan.jumlah + " = Rp " + totalPesanan);
            totalBayar += totalPesanan;
        }

        System.out.println("Total Bayar: Rp " + totalBayar);
        System.out.println("Terima kasih telah berkunjung!");

        scanner.close();
    }
}
