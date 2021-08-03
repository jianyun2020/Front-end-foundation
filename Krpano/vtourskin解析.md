
# action

## skin_loadscene

缩略图点击跳转相应的全景图

```xml
<action name="skin_loadscene" scope="local" args="newscenenameorindex, blendmode">

    if(webvr.isenabled AND scene.count GT 1,

    set(hotspot[skin_webvr_prev_scene].visible, false);

    set(hotspot[skin_webvr_next_scene].visible, false);

    );



    calc(layer[skin_thumbborder].parent, 'skin_thumb_' + scene[get(newscenenameorindex)].index);

    layer[skin_thumbs].scrolltocenter(get(scene[get(newscenenameorindex)].thumbx),

    get(scene[get(newscenenameorindex)].thumby));

    loadscene(get(scene[get(newscenenameorindex)].name), null, get(skin_settings.loadscene_flags), get(blendmode));



    <!--点击热点菜单状态更新-->

    <!-- js( menuCtrl(get(scene[get(xml.scene)].name), get(scene[get(xml.scene)].title), get(scene[get(xml.scene)].datamark)) ); -->

    <!--点击热点菜单状态更新-->


    <!-- if(show == null, if(layer[skin_thumbs].state == 'closed', set(show,true), set(show,false)); );

    if(show,

    set(layer[skin_thumbs].state, 'opened');

    tween(layer[skin_thumbs].alpha, 1.0, 0.25);

    tween(layer[skin_scroll_layer].y, calc(-area.pixelheight + layer[skin_thumbs].height +

    layer[skin_scroll_layer].y_offset), 0.5, easeOutQuint);

    set(layer[skin_thumbs_container].visible, true);

    tween(layer[skin_thumbs_container].alpha, 1.0, 0.25);

    tween(layer[skin_map].alpha, 0.0, 0.25, default, set(layer[skin_map].visible,false));

    ,

    set(layer[skin_thumbs].state, 'closed');

    tween(layer[skin_thumbs].alpha, 0.0, 0.25, easeOutQuint);

    tween(layer[skin_scroll_layer].y, calc(-area.pixelheight + layer[skin_scroll_layer].y_offset), 0.5,

    easeOutQuint, set(layer[skin_thumbs_container].visible, false););

    ); -->

  </action>
```