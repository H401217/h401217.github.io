```smali

#replace [NAME] with your file name

.class public Ly8/[NAME];
.super Lx8/a;
.source "SourceFile"

#max potion
#y8/g clone

# direct methods
.method public constructor <init>()V
    .locals 3

    const/16 v0, 0x63 #price?
    const/4 v1, 0x1
    const/16 v2, 0x8 #ID of your potion

    invoke-direct {p0, v2, v0, v1}, Lx8/a;-><init>(III)V

    return-void
.end method


# virtual methods
.method public l(Lq9/a;Lv3/a;Lme/pou/app/AppView;)Z #main function
    .locals 5

    iget-wide v0, p1, Lq9/a;->k:D #hunger
    const-wide v2, 0x4056800000000000L    # 90.0
    cmpg-double v4, v0, v2
    if-ltz v4, :cond_1

    iget-wide v0, p1, Lq9/a;->p:D #health
    cmpg-double v4, v0, v2
    if-ltz v4, :cond_1

    iget-wide v0, p1, Lq9/a;->u:D #fun
    cmpg-double v4, v0, v2
    if-ltz v4, :cond_1

    iget-wide v0, p1, Lq9/a;->x:D #sleep
    cmpg-double v4, v0, v2
    if-gez v4, :cond_0

    goto :goto_0

    :cond_0 # Pou doesnt need that
    const/4 p1, 0x0

    return p1

    :cond_1 # Pou needs that
    :goto_0
    const/16 v0, 0x64

    invoke-virtual {p1, v0, p2, p3}, Lq9/a;->v(ILv3/a;Lme/pou/app/AppView;)V #hunger
    invoke-virtual {p1, v0, p2, p3}, Lq9/a;->z(ILv3/a;Lme/pou/app/AppView;)V #health
    invoke-virtual {p1, v0, p2, p3}, Lq9/a;->w(ILv3/a;Lme/pou/app/AppView;)V #fun
    invoke-virtual {p1, v0, p2, p3}, Lq9/a;->u(ILv3/a;Lme/pou/app/AppView;)V #sleep

    const/16 v0, 0x32

    invoke-virtual {p1, v0, p3}, Lq9/a;->a(ILme/pou/app/AppView;)V #potion end (probably effect)

    invoke-super {p0, p1, p2, p3}, Lx8/a;->l(Lq9/a;Lv3/a;Lme/pou/app/AppView;)Z
    move-result p1
    return p1
.end method

.method public n()Ljava/lang/String; #Title
    .locals 1

    const v0, 0x7f1102fe #description

    invoke-static {v0}, Lme/pou/app/App;->h1(I)Ljava/lang/String;
    move-result-object v0
    return-object v0
.end method

.method public o()Ljava/lang/String; #Description
    .locals 1

    const v0, 0x7f1102fd #title

    invoke-static {v0}, Lme/pou/app/App;->h1(I)Ljava/lang/String;
    move-result-object v0
    return-object v0
.end method
```