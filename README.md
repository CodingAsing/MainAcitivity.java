package com.example.programpenjualan;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

  EditText namabrg,hargabrg,jumlahbrg,pembayaran;
  TextView total,kembalian,totalbayar;
  Button payment,Total,clear;

    private String[] Item = {"Bank","E-Wallet","Tunai"};
    private String[] jenis = {"Laptop","Handphone","Accesoris"};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        namabrg = (EditText) findViewById(R.id.namabrg);
        hargabrg =(EditText) findViewById(R.id.hargabrg);
        jumlahbrg =(EditText) findViewById(R.id.jumlahbrg);
        pembayaran =(EditText) findViewById(R.id.tunai);
        total = (TextView) findViewById(R.id.totalbrg);
        kembalian = (TextView) findViewById(R.id.kembalian);
        totalbayar = (TextView) findViewById(R.id.totalbayar);
        payment =(Button) findViewById(R.id.payment);
        Total = (Button) findViewById(R.id.Total);
        clear = (Button)findViewById(R.id.clear);

        final Spinner List2 = findViewById(R.id.jenis);
        final Spinner List = findViewById(R.id.pembayaran);

        final ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
                R.layout.activity_spinner,Item);
        List.setAdapter(adapter);
        List.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override

            public void onItemSelected(AdapterView adapterView, View view, int i, long l) {

            }

            @Override
            public void onNothingSelected(AdapterView adapterView) {

            }
        });
        final ArrayAdapter<String> adapter2 = new ArrayAdapter<String>(this,
                R.layout.activity_spinner,jenis);
        List2.setAdapter(adapter2);
        List2.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView adapterView, View view, int i, long l) {
            }

            @Override
            public void onNothingSelected(AdapterView adapterView) {
            }
        });

        Total.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Double harga,jumlah,totalbarang;

                harga = Double.valueOf(hargabrg.getText().toString().trim());
                jumlah = Double.valueOf(jumlahbrg.getText().toString().trim());

                totalbarang = harga*jumlah;
                String total1 = String.valueOf(totalbarang);
                total.setText(total1);
            }
        });

        payment.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Double tunai,totalbarang, kembaliantunai,ppn,totalb;

                tunai = Double.valueOf(pembayaran.getText().toString().trim());
                totalbarang = Double.valueOf(total.getText().toString().trim());

                ppn = totalbarang * 10/100;
                totalb = totalbarang + ppn;
                kembaliantunai = tunai-totalb;

                String kembali = String.valueOf(kembaliantunai);
                String totalplus = String.valueOf(totalb);

                totalbayar.setText(totalplus);
                kembalian.setText(kembali);


            }
        });

        clear.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                namabrg.setText("");
                hargabrg.setText("");
                jumlahbrg.setText("");
                pembayaran.setText("");
                total.setText("");
                kembalian.setText("");
                totalbayar.setText("");
            }
        });

    }

}
