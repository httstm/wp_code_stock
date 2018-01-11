```
// ごく単純に。
$my_query = new WP_Query(array('category_name' => '(カテゴリスラッグ)','posts_per_page' => '(一度に表示させたい件数)'));
if($my_query->have_posts()):
    while($my_query->have_posts()):$my_query->the_post();
        if(mb_strlen(get_the_content()) !==0 ){
            $view_date = '<a href="'.get_the_permalink().'">'.get_the_date().'</a>';
        }else{
            $view_date = get_the_date();
        }	
        // echo the_date().'<br>';
        echo $view_date.'<br>';
        echo get_the_title();
        echo '<hr>';
    endwhile;
endif;
wp_reset_postdata();
```

参考:
[Codex WP_Query](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/WP_Query#.E3.82.AB.E3.83.86.E3.82.B4.E3.83.AA.E3.83.BC.E3.81.AE.E3.83.91.E3.83.A9.E3.83.A1.E3.83.BC.E3.82.BF)
