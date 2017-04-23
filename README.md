# potherca-abandoned.github.io

<ul id="list"></ul>

<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/elusive-icons/2.0.0/css/elusive-icons.min.css" />
<link rel="stylesheet" href="https://pother.ca/CssBase/css/base.css" />
<link rel="stylesheet" href="https://pother.ca/embed-jsfiddle-result-on-potherca.css" />

<script
  crossorigin="anonymous"
  integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="
  src="https://code.jquery.com/jquery-1.12.4.min.js"
></script>
 

<script>
var $List = $('#list'),
    sUser ='potherca-abandoned',
    sUrl = 'https://api.github.com/users/' + sUser + '/repos?per_page=100' //@TODO: Once there are more than a hundred repos for a user this needs to be resolved by parsing the "Link" HTTP header send with the response
;

$.ajax({
    dataType: "json",
    url: sUrl,
    success: function(p_oData, p_sStatus, p_oRequest){
        $.each(p_oData, function(p_iIndex, p_oRepo){
            var sHomepageLink='';
            if(p_oRepo.fork === false){
                if(p_oRepo.homepage){
                    sRepoName = '<a href="' + p_oRepo.homepage + '" target="_blank">' + p_oRepo.name  + '</a> '
                } else {
                    sRepoName = '<a title="Click the Github icon to visit this repo" target="_blank">' + p_oRepo.name  + '</a> '
                }                    
                $List.append(
                      '<li>' 
                        + ' <a href="' + p_oRepo.html_url + '" class="el el-github" target="_blank"></a>'
                        + sRepoName
                        + '<span class="description">' + p_oRepo.description + '</span>'
                    + '</li>'
                );
            }
        });
    },
    error: function(p_oJqXHR, p_sStatus, p_sError){
        $List.append('<li class="error">' + p_sError + ': ' + p_sStatus + '</li>');
    }
});

/*EOF*/
</script>
