// challenge

/* # Live Code - Javascript


## Requirement

Buatlah fungsi kulkas yang dapat:

### Fungsi `kulkas`

Fungsi ini berguna untuk membangun kulkas pertama kali, dengan rincian sebagai berikut:

- Menentukan kapasitas kulkas sesuai dengan parameternya.
- Pembuatan kulkas ini memerlukan waktu sebanyak 5000ms.
- Mengembalikan 3 actions yaitu, `put`, `take`, dan `check`.

### Fungsi `put`

Fungsi ini berguna untuk memasukkan makanan kedalam kulkas, dengan rincian sebagai berikut:

- Mendaftarkan makanan yang akan dimasukkan kulkas, berupa object `Groceries`, dengan property `id` dan `nama`.
- Terdapat validasi jika makanan dengan id tertentu sudah didalam kulkas, maka makanan tersebut tidak dapat dimasukkan.
- Terdapat validasi jika kapasitas kulkas penuh maka makanan tidak dapat masuk ke kulkas.
- proses memasukkan setiap satuan makanan ini memerlukan waktu 3000ms.

### Fungsi `take`

Fungsi ini berguna untuk mengeluarkan makanan dari kulkas, dengan rincian sebagai berikut:

- Melakukan take groceries berdasarkan `id` makanan.
- Terdapat validasi `id` makanan, yang bisa keluar hanya makanan yang `id`-nya sudah terdaftar masuk ke kulkas.
- proses mengeluarkan setiap satuan makanan memerlukan waktu 1500ms

### Fungsi `check`

Fungsi ini akan menampilkan informasi kapasitas kulkas, sisa slot kulkas yang kosong, dan makanan yang ada didalam kulkas.

- Proses check ini memerlukan waktu 500ms.
- Proses check akan mengembalikan object `Kulkas`.

## Objects

### Grocery

```Javascript
class Grocery {
    constructor
  id;    // Id bahan makanan
  name;  // Nama bahan makanan
}
```

### Kulkas

```Javascript
class Kulkas {
  capacity;   // Kapasitas kulkas
  remaining;  // Sisa tempat kulkas yang masih kosong
  groceries;       // Array dari object Grocery.
}
```

### Command Output Sample

#### Command
<!-- contoh jika urutan skenario yang diinginkan: -->

```Javascript
createKulkas -> 3 
put -> makanan1 
check
put -> makanan2 
leave -> B2021
put -> makanan3
put -> makanan4
take -> B2019
put -> makanan5
put -> makanan1
take -> B2021
check
take -> BE001
check
```
    
#### Output
<!-- contoh output dari skenario diatas -->

```Javascript
Kulkas berhasil dibuat dengan kapasitas 3 makanan
Makanan dengan id BE001 berhasil dimasukkan.
{ capacity: 3, remaining: 2, puttedGroceries: [makanan1] }
Makanan dengan id B2021 berhasil dimasukkan.
Makanan dengan id B2021 sudah keluar.
Makanan dengan id C012 berhasil dimasukkan.
Makanan dengan id D0101 berhasil dimasukkan.
Makanan dengan id B2019 tidak ada.
Mohoh maaf kulkas sudah penuh.
Makanan dengan id BE001 sudah dimasukkan sebelumnya.
Makanan dengan id B2021 tidak ada.
{ capacity: 3, remaining: 0, puttedGroceries: [makanan1, makanan3, makanan4] }
Makanan dengan id BE001 sudah keluar.
{ capacity: 3, remaining: 1, puttedGroceries: [makanan3, makanan4] } 
```
 */

// jawab 

class Grocery {
    constructor(id,name) {
        this.id = id;
        this.name = name;

    }
}


class Kulkas  {
    constructor(capacity){
        this.capacity = capacity ;
        this.remaining = capacity;
        this.groceries = [];
    } 

    } 

     const createKulkas = (capacity, actions) => {
         let newKulkas = new Kulkas(capacity);

         const put = (Grocery, callback) => {
             setTimeout(() => {
                 if(newKulkas.remaining < 1){
                 callback(`Mohon maaf kulkas sudah penuh`)
                 } else {
                     if (newKulkas.groceries.id === Grocery.id){
                         callback(`tidak bisa masuk`)
                     } else{
                newKulkas.groceries.push(Grocery)
                newKulkas.remaining -= 1;
                callback(`Makanan dengan id ${Grocery.id} dan nama ${Grocery.name} berhasil dimasukkan`)   
                 }
                }
             }, 3000)
            
         }

         const take = (id, callback) => {
             setTimeout(() => {
                if(newKulkas.groceries.id === id) {
                 let Kulkas = newKulkas.groceries.find((Kulkas) => Kulkas.id == id )
                 newKulkas.groceries.splice(newKulkas.groceries.indexOf(Kulkas, 1))
                 newKulkas.remaining += 1;
                 callback (`Makanan dengan id ${id} dikeluarkan`)
                 }else {
                     callback(`makanan dengan ${id} tidak ada`)
                 }
             }, 1500)
             
        }

        const check = (callback) => {
            setTimeout(() =>{
                callback(newKulkas);
            }, 500)
        }

        setTimeout(() =>{
            console.log(`Berhasil membuat kulkas dengan kapasitas ${capacity} makanan`);
            actions(put, take, check)
        })

    }

    let apel  = new Grocery("001", "Apel"); // membuat object makanan yang ingin dimasukkan
    let jeruk = new Grocery("002", "jeruk");
    let nanas = new Grocery("003", "Nanas");

     createKulkas(3, (put, take, check) => {
         check((output)=> {
             console.log(output);
             put(apel,(message) => {
                 console.log(message);
                 check((output)=>{
                     console.log(output);
                     take("001", (message) =>{
                         console.log(message);
                         check((output) =>{
                             console.log(output);
                             put(jeruk,(pesan) =>{
                                 console.log(pesan);

                                 take("001",(message) =>{
                                     console.log(message);

                                     check((output)=>{
                                        console.log(output);
                            })
                        })
                     })
                 })
             })
         })
    })
 })
});
