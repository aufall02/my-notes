# Laravel

## Eloquent model returns 0 as primary key

secara default primary key di laravel  akan dibuat auto increment, jika menggunakan primary key string maka kita harus meng set models kita seperti dibawah agar returnya tidak 0
```
protected $keyType = 'string';
public $incrementing = false;
```

