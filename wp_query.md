<?php 
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
?>