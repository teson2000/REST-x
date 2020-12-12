# Breakout
Evaluation of design.

## Goal
Self hosted collaboration management.

## Endpoints

    GET /groups
    POST /groups
    GET /groups/{group-id}
    GET /groups/{group-id}/overview
    PUT /groups/{group-id}/cover_image
    POST /groups/{group-id}/doSendInvite
    GET /groups/{group-id}/members
    GET /groups/{group-id}/photos
    GET /groups/{group-id}/posts
    GET /groups/{group-id}/events
    GET /groups/{group-id}/photos/{photo-id}    
    GET /groups/{group-id}/members/{member-id}
    
    GET /member/{member-id}/photos
    
    POST /session/doLogin
    POST /session/doLogout
    GET /session/who_am_i
    GET /session/users
    
    GET /admin/settings
    POST /admin/reg_svr
    
    GET /api/ping
    POST /api/doPing
    GET /api/status
    POST /api/doRestart
    
    
