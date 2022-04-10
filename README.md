# remote2local
codeigniter远程图片本地化helper

## 微信头像本地化

```php
$headimgurl = $userinfo['headimgurl'];
    	            
    	            // 头像本地化
    	            if(!empty($userinfo['headimgurl'])){
    	                $base_url = config_item('cdn_server1') . 'resource/upfiles/mp/headimg/';
    	                $file_path = FCPATH . 'resource/upfiles/mp/headimg/' . date('Y') . '/' . date('md') . '/';
    	                
        	            $this->load->helper('remote2local');
        	            $response = remoteimg($userinfo['headimgurl']);
    					if($response && $response['http_code'] == '200'){
    						$content_type = $response['content_type'];
    						$filename3 = md5($openid);
    						switch($content_type){
    							case 'image/jpeg':
    							case 'image/jpg':
    							case 'image/pjpeg':
    								$filename1 =  $file_path . $filename3 . '.jpg'; 
    								$filename2 =  $base_url . date('Y') . '/' . date('md') . '/' . $filename3 . '.jpg';
    								break;
    							case 'image/gif':
    								$filename1 = $file_path . $filename3 . '.gif'; 
    								$filename2 = $base_url . date('Y') . '/' . date('md') . '/' . $filename3 . '.gif'; 
    								break;
    							case 'image/png':
    							case 'image/x-png':
    								$filename1 = $file_path . $filename3 . '.png'; 
    								$filename2 = $base_url . date('Y') . '/' . date('md') . '/' . $filename3 . '.png'; 
    								break;
    							case 'image/bmp':
    								$filename1 = $file_path . $filename3 . '.bmp';
    								$filename2 = $base_url . date('Y') . '/' . date('md') . '/' . $filename3 . '.bmp';
    								break;
    						}
    						mkdir_r(dirname($filename1));
    						file_put_contents($filename1, $response['content']);
    						$headimgurl = $filename2;						
    					}
    	            }
```
