# SPASE-JPCOAR

This project provide XSLT stylesheets that transforms [SPASE](https://spase-group.org/) metadata into [JPCOAR](https://jpcoar.repo.nii.ac.jp/) metadata.

## Description

SPASE は Heliophysics データを交換するためのオープンな標準を提供しており、その標準メタデータスキーマは日本国内でも関連研究分野で利用されています。一方、 JPCOAR は国内の研究成果を集積する機関リポジトリを運営しています。 JPCOAR スキーマに従ってメタデータを記述することで研究成果を機関リポジトリに登録することができます。

ここで提供する XSLT スタイルシートを利用すると、研究データの交換用に作成したSPASE メタデータから機関リポジトリ登録用の JPCOAR メタデータを自動的に生成することができるため、新たに JPCOAR メタデータを書き直す必要がありません。

SPASE provides open standards for exchanging Heliophysics data, and its standard metadata schema is widely used in Japan in related research fields. On the other hand, JPCOAR operates an institutional repository that collects research results in Japan. Research results can be registered in the institutional repository by describing metadata according to the JPCOAR schema.

By using the XSLT stylesheet provided here, JPCOAR metadata for institutional repository registration can be automatically generated from SPASE metadata created for research data exchange, eliminating the need to rewrite new JPCOAR metadata.

## Getting Started

Prepare an XSLT processor. For Ubuntu, we recommend to use xsltproc.

```
$ sudo apt install xsltproc
```

Executes the conversion process on the command line. The first parameter specifies the XSLT stylesheet to be used, and the second parameter specifies the XML file of SPASE metadata to be converted. The results of the conversion will be displayed on standard output, so if you wish to save the file, redirect to the file.

```
$ xsltproc spase2jpcoar.xsl spase_sample.xml > jpcoar_sample.xml
```

We now offer the following two style sheets;
- `spase2jpcoar.xsl` Convert from SPASE 2.4.0 to JPCOAR v1.0.2
- `spase2jpcoar2_0.xsl` Convert from SPASE 2.6.1 to JPCOAR v2.0.0

## Notes

これらのスタイルシートには、 `publisher` 要素の値として「名古屋大学 / Nagoya University」が埋め込まれています。他の機関で利用する場合、この部分をテキストエディタ等で書き換えてご利用ください。

These stylesheets have “名古屋大学 / Nagoya University” embedded as the value of the `publisher` element. When using them at other institutions, please edit this portion using a text editor or similar tool.

        <dc:publisher xml:lang="ja">名古屋大学</dc:publisher>
        <dc:publisher xml:lang="en">Nagoya University</dc:publisher>

`xsltproc` コマンドで変換した XML 文書は改行やインデントを含みません。読みやすく整形した XML にしたい場合は、 `xmllint` コマンドを利用してください。

XML documents transformed using the `xsltproc` command do not include line breaks or indentation. To obtain well-formed XML for readability, use the `xmllint` command.

```
$ sudo apt install libxml2-utils
$ xsltproc spase2jpcoar.xsl spase_sample.xml | xmllint --format - > jpcoar_sample.xml
```

## Authors

[IUGONET project team](http://www.iugonet.org/contact/)

## License

This project is licensed under the [MIT](https://opensource.org/license/mit) License - see the LICENSE.md file for details

## References

- [SPASE Base Model Schema](https://spase-group.org/data/schema/)
- [JPCOAR Schema](https://schema.irdb.nii.ac.jp/)
